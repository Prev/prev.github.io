---
title: styled-components + Storybook + TypeScript로 React 컴포넌트 관리하기
description: styled-components + Storybook + TypeScript로 React 컴포넌트 관리하기
tags: ['프론트엔드']
image: sc-st-on-react/cover.jpg
---

제니퍼소프트에서 인턴을 하면서 제품 내의 컴포넌트가 너무 비대해지고 CSS dependency도 복잡하게 얽혀있어 정리가 필요한 시점이 오고 있었다. 이에 <u>① 컴포넌트의 재사용을 쉽게 하고</u> <u>② 꼬여있던 스타일을 정리하며</u> <u>③ 테스트 코드 작성까지 용이</u>하도록 주요 컴포넌트를 분리하기로 하였고, [styled-components](https://www.styled-components.com/)와 [Storybook](https://storybook.js.org/)을 이용하기로 하였다. 또 기존 코드에서 TypeScript를 사용하고 있었기에 분리한 컴포넌트들도 마찬가지로 TypeScript를 이용하기로 했다.



## styled-components

<p class="center">
  <img src="/attachs/sc-st-on-react/styled-components.png" width="220" height="220">
</p>

React에서 컴포넌트 스타일링을 하는 방법에는 여러 가지가 있다. 가장 간단한 방법으로 `.css` 파일을 import 하거나, Sass/SCSS 등 CSS Preprocessor를 사용하는 방법, 여기에 CSS module을 이용하는 방법, `CSS-in-JS` 라이브러리를 이용하는 방법 등이 있다. 자세한 내용은 [이 글](https://velog.io/@velopert/react-component-styling)에 정리가 잘 되어있다.

우리는 CSS-in-JS 라이브러리 중 가장 핫한 [**styled-components**](https://www.styled-components.com/)를 사용하기로 했다. styled-components에서는 `tagged template literal` 이라는 syntax를 이용하여 스타일을 정의하게 되는데, JavaScript에서 스타일을 줄 때 보통 object로 주었던 것과 비교해서 훨씬 깔끔하고 CSS의 문법 거의 그대로를 적용시킬 수 있어서 마이그레이션도 꽤 편리하다.

```jsx
import styled from 'styled-components';

const Button = styled.button`
  background: transparent;
  border: 2px solid palevioletred;
  color: palevioletred;
  padding: 0.25em 1em;
`;

const Container = (props) => (
  <Button />
);
```

위 코드처럼 스타일을 줄 때 HTML 기본 태그(div, span, button, ...)를 확장하는 형태로 기술하게 되며, 만들어진 컴포넌트는 React Component 처럼 이용할 수 있다.

만들어진 스타일 컴포넌트는 고유의 `className`을 갖게 되며(`sc-VigVT` 같은 형태), 자동으로 생성되기에 관리의 필요성이 사라진다. 기존 CSS/SCSS 방식은 stylesheet만 보고 어떤 컴포넌트가 이 스타일을 쓰는지 명확히 알기가 어려웠지만 styled-component를 이용하면 그런 문제가 발생하지 않기에 코드의 가독성을 향상시키며 협업을 용이하게 하기도 한다.



또한 SCSS의 문법과 유사하게 스타일을 줄 수도 있는데, 컴포넌트 내부의 자식의 스타일을 지정한다거나, `:hover`, `:before`, `:nth-child` 등 가상 선택자도 사용이 가능하다. 이는 곧 컴포넌트와 스타일을 1:1로 매핑할 필요 없이 `className`이나 `id`을 혼재하여 스타일을 줄 수 있다는 의미인데, 상황에 따라 **유연하게** 스타일을 작성할 수 있다는 점에서 꽤 편리함을 보였다.

```js
const SearchWrapper = styled.div`
  position: relative;
  font-size: 12px;
  border-radius: 4px;

  span.icon {
    line-height: 32px;
    cursor: pointer;

    &:hover {
      color: #49f;
    }
  }
`;
```

다만 이 유연함이 어디까지 분리를 해서 스타일 컴포넌트로 만들어야 하는가에 대해서 고민해야 하는 상황을 만들기도 한다. 특히  `className`을 무분별하게 사용하다 보면 기존에 CSS를 사용하며 발생했던 '의도치 않은 태그에 스타일이 적용되는 상황'이 다시 발생하기에 주의깊게 사용해야 할 것이다.



### TypeScript와 함께 props 사용하기

styled-components의 또 다른 주요한 특징은 `props`를 바탕으로 한 [조건부 스타일링](https://www.styled-components.com/docs/basics#adapting-based-on-props)이 가능한 점이다. 같은 컴포넌트여도 **특징에 따라(크기, 테마, 방향 등) 조금씩 다르게 렌더링** 될 수 있는데, 매번 새로운 컴포넌트를 만드는 것은 비효율적이다. styled-components 에서는 `template literal` 내에 `${props => /* expression */};` 형태의 문법을 이용하여 주어진 props에 따라 다른 CSS를 렌더링하도록 할 수 있다.

여기서의 `props`은 React 컴포넌트의 props과 대응된다. TypeScript에서 React 컴포넌트의 props에 `type`을 정의해주어야 하는 것처럼 styled-component의 props도 type을 정의해주어야 한다. 이도 마찬가지로 *Generic*을 이용해서 지정해주면 type 검사와 힌트가 알맞게 뜨며 TypeScript의 강점을 그대로 이용할 수 있다.

```ts
interface ButtonPropsType {
  primary?: boolean;
}

const Button = styled.button<ButtonPropsType>`
  background: ${props => props.primary ? "palevioletred" : "white"};
  color: ${props => props.primary ? "white" : "palevioletred"};
  padding: 0.25em 1em;
  border: 2px solid palevioletred;
`;

const Container = (props: {}) => (
  <Button>Hello</Button>
  <Button primary>Hello</Button>
);
```

위 코드를 주의 깊게 살펴보면 `props` 값이 변수 형태로 passing 되지 않고, 일종의 **call-back 함수**가 passing 되는 것을 볼 수 있다. `background: ${props.primary}` 와 같이 사용하지 않는다는 점에 유의해야 한다. 이 때문에 조건부 코드가 조금 길어지기는 하지만, 아래 코드처럼 여러 조건에 따른 분기 처리나 CSS block 단위의 조작 등 더 자유롭게 조건에 따른 스타일을 지정해줄 수 있다.

```js
const Button = styled.button`
  background-color: transparent;

  ${props => props.primary && !props.transparent &&
    css`
      background-color: ${props.theme.primary || '#497eff'};
      color: #fff;
    `};

  ${props => props.primary && props.transparent &&
    css`
      background-color: transparent;
      color: ${props.theme.primary || '#497eff'};
    `};
```



### 컴포넌트 상속

`props`에 따른 조건부 스타일링과는 별개로, **스타일링 된 컴포넌트 자체를 상속받아** 구현해야 할 상황도 존재할 수 있다. 이런 경우에도 styled-components 에서는 **확장(extending)** 기능을 제공하므로써 훌륭하게 문제를 해결할 수 있다. 기존에 만들어진 컴포넌트를 `styled` 생성자(constructor)로 감싼 후 `template literal`을 뒤에 적어주면 기존 스타일 컴포넌트를 상속받은 새로운 컴포넌트를 정의할 수 있다.

```js
const TomatoButton = styled(Button)`
  color: tomato;
  border-color: tomato;
`;
```

TypeScript에서도 상속은 훌륭하게 동작하는데, 상속받은 새로운 컴포넌트가 `props`를 부모와 다르게 가져갈 때에도 Generic을 통해 타입을 지정해주면 문제없이 사용할 수 있다.

```ts
interface PrimaryButtonPropsType extends ButtonPropsType {
  xlarge?: boolean;
}

const PrimaryButton = styled(Button)<PrimaryButtonPropsType>`
  color: white;
  border-color: blue;

	${props => props.xlarge &&
    css`
      font-size: 20px;
      height: 64px;
      line-height: 64px;
    `};
`;
```



## Storybook

<p class="center">
  <img src="/attachs/sc-st-on-react/storybook.png" width="400">
</p>

[스토리북(Storybook)](https://storybook.js.org/)은 UI 컴포넌트를 독립적인 환경에서 개발을 돕는 오픈소스 툴이다. React 뿐만 아니라 Vue, Angular 프레임워크도 지원하며 다양한 애드온을 기반으로 **UI 컴포넌트**를 쉽게 테스트할 수 있도록 돕는다. 

Single Page Application(SPA) 개발을 진행하다 보면 컴포넌트를 중심적으로 코드를 작성하게 되며, 프로젝트가 커지고 요구 사항이 복잡해짐에 따라 컴포넌트 간의 관계가 매우 복잡해지게 된다. 이런 상황 속에서 각 컴포넌트의 기능이 어디까지이고 속성에 따라 어떻게 변화하는지 알기가 어려워지는 경우가 많다. **컴포넌트 관리가 필요하지만 *documentation*까지 하기는 어려운 상황에 Storybook을 이용한다면 적은 비용으로 유사한 혜택**을 얻을 수 있다.

![storybook-screenshot](/attachs/sc-st-on-react/storybook-screenshot.png)



### 스토리 (Stories)

Storybook에서 컴포넌트를 이용하여 그 사용법 등을 보여주는 코드를 스토리(Stories)라 부른다. `*.stories.js` 같은 확장자를 이용하여 컴포넌트와 같은 위치에 작성할 수도 있고, 별개의 `stories` 디렉토리를 만들어서 적어줄 수도 있다. 코드는 아래처럼 생겼으며, 보통 <u>컴포넌트 단위마다</u> 스토리를 적어준다.

```jsx
import React from 'react';
import { storiesOf } from '@storybook/react';
import { action } from '@storybook/addon-actions';
import Button from '../components/Button';

storiesOf('Button', module)
  .add('with text', () => (
  	<Button onClick={action('clicked')}>Hello Button</Button>
	)
  .add('with some emoji', () => (
    <Button onClick={action('clicked')}>
      <span role="img" aria-label="so cool">
        😀 😎 👍 💯
      </span>
    </Button>
  ));
```

스토리는 컴포넌트에 대한 기술(description) 코드라고 볼 수 있다. 컴포넌트에 어떤 `props`를 주었을 때 어떻게 나타나는지, 특정한 액션을 취했을 때 (클릭, 마우스오버, 포커스 등) 컴포넌트가 어떻게 변화하는지 등을 standalone하게 보고 테스트할 수 있게 해준다. 스토리 코드는 **곧 컴포넌트에 대한 훌륭한 사용 예시**이기도 하므로, 다수의 프론트엔드 개발자가 참여하는 프로젝트라면 이를 통해 코드의 이해에 대한 장벽을 낮춤과 동시에 커뮤니케이션 코스트 또한 낮출 수 있을 것이다.



### 애드온 (Add-on)

Storybook의 핵심은 애드온이라고 할 수 있다. 애드온을 잘 쓰지 못하면 그저 새로운 React App를 만들고 해당 앱에 컴포넌트를 나열 한 것과 크게 다를 게 없다. Storybook에서 제공하는 주요 애드온에는 아래가 있다.

- [a11y](https://github.com/storybookjs/storybook/tree/master/addons/a11y): 접근성(accessibility) 테스트
- [Actions](https://github.com/storybookjs/storybook/tree/master/addons/actions): 컴포넌트에서 `props`를 통해 받는 이벤트에 바인딩하여 그 로그를 패널에 보여주는 애드온
- [Knobs](https://github.com/storybookjs/storybook/tree/master/addons/knobs): `props`를 스토리북에서 유저가 동적으로 바꿀 수 있도록 하는 애드온. `text`, `number`, `select`, `boolean` 등 다양한 타입을 제공한다
- [Backgrounds](https://github.com/storybookjs/storybook/tree/master/addons/backgrounds): 배경 색상을 바꿀 수 있게 해주는 애드온
- [Viewport](https://github.com/storybookjs/storybook/tree/master/addons/viewport): 디바이스 viewport를 바꿀 수 있는 애드온. 반응형 컴포넌트 개발 시 테스트하기 용이하게 해줌

이 밖에도 다양한 애드온이 존재하며 [이곳](https://storybook.js.org/docs/addons/addon-gallery/)에서 확인할 수 있다.

애드온을 적절히 활용하면 스토리를 작성하는 비용이 크게 줄어든다. 예를 들어 <u>Knobs</u>을 잘 활용하면 조건에 따른 컴포넌트를 무수히 나열할 필요가 없어지며, <u>Actions</u>를 이용하면 이벤트 처리에 대한 함수를 따로 작성하지 않아도 된다. 아래 코드처럼 작성하면 Storybook 하단 패널에 message, position, disabled 값을 입력받을 수 있는 창이 나타나고, 그 값에 따라 Tooltip 컴포넌트를 렌더링 시키게 된다. Tooltip 이 나타나면 Actions탭에 onActive 메시지가 이벤트 파라미터와 함께 보이게 된다.

```js
import { storiesOf } from '@storybook/react';
import { action } from '@storybook/addon-actions';
import { text, boolean, select, withKnobs } from '@storybook/addon-knobs';

storiesOf('Tooltip', module)
    .addDecorator(withKnobs)
    .add('tooltip', () => {
        const message = text('message', 'Hello Label!');
        const position = select('position', ['top-left', 'top-right', 'bottom-left', 'bottom-right'], 'top-left');
        const disabled = boolean('disabled', false);

        return (
          <Tooltip
            message={message}
            position={position}
            disabled={disabled}
            onActive={action('Tooltip onActive')}
          >
            <span>Content</span>
          </Tooltip>
        )
	  })
```

애드온은 대부분 이처럼 별도의 Panel에서 UI로 값을 보여주거나 입력받을 수 있게 해주는데, 이를 통해 개발자 이외에도 **디자이너나 QA 인력이 다양한 값을 직접 입력해보며 테스트를 진행할 수 있게 된다.** 제품에서 컴포넌트를 사용하는 시나리오 외에도 다양한 edge-case 들을 테스트하기 용이하므로, Storybook을 이용한다면 보다 **robust 한 컴포넌트를 개발**을 할 수 있게 된다.

<p class="center">
  <img src="/attachs/sc-st-on-react/storybook-knobs.png" alt="storybook-knobs" width="425">
  <span class="caption">Kbobs 애드온을 통해 다양한 타입의 props를 입력받을 수 있다.</span>
</p>


또한 Storybook은 [애드온 API](https://storybook.js.org/docs/addons/api/)를 제공하기에 기본으로 제공하는 것 이외에도 직접 애드온을 개발하여 사용할 수도 있다. 진행했던 프로젝트의 경우에는 *테마*를 선택할 수 있는 애드온을 만들어 사용하기도 하였다.

### TypeScript와 함께 사용하기

Storybook 및 기본 애드온들 모두 [DefinitelyTyped](https://github.com/DefinitelyTyped/DefinitelyTyped)에서 등록되어 있어 TypeScript를 사용하는데 styled-components와 마찬가지로 문제없이 파워풀하게 기능들을 이용할 수 있다. 다만 약간의 설정이 필요한데, Storybook에서 내부적 사용하는 webpack의 config를 확장하여 `.ts|.tsx` 파일에 대해 `ts-loader`를 이용하도록 구성해주어야 한다. [공식 문서](https://storybook.js.org/docs/configurations/typescript-config/)에서도 친절히 나와있어 설정하는데 큰 어려움은 없을 것이다.

```js
// .storybook/webpack.config.js
module.exports = ({ config, mode }) => {
    config.module.rules.push({
        test: /\.tsx?$/,
        use: [
            { loader: require.resolve('babel-loader') },
            { loader: require.resolve('ts-loader') },
        ]
    });
    config.module.rules.push({
        test: /\.stories\.tsx?$/,
        loaders: [
            {
                loader: require.resolve('@storybook/addon-storysource/loader'),
                options: { parser: 'typescript' },
            },
        ],
        enforce: 'pre',
      });
    config.resolve.extensions.push('.ts', '.tsx');
    return config;
  };

```

나는 스토리 파일들을 `/stories` 디렉토리에 `*.stories.tsx` 와 같은 규칙으로 만들어 주고 있었기에, 아래처럼 config 파일에서 적합한 파일들을 불러오도록 작성해주기도 하였다.

```js
// .storybook/config.tsx
const req = require.context('../stories', true, /\.stories\.tsx$/);

configure(() => {
    req.keys().forEach(req);
}, module);
```





## 패키징 및 배포

이렇게 작성한 컴포넌트는 <u>재사용</u>을 위해 기존 제품에서 **분리**하여 **별도의 프로젝트**로 만들게 되었다. 분리된 컴포넌트를 기존 제품에서 불러와 사용할 수 있도록 만들기 위해 패키징 작업이 필요했는데, Storybook에 기반한 프로젝트 특성상 크게 2가지 종류로 나누어 패키징 및 배포 작업을 해야했다.

1. **Storybook**: 팀원들이 컴포넌트를 보고 테스트할 수 있도록 웹 형태로 제공
2. **컴포넌트**: 다른 node 프로젝트에서 사용할 수 있도록 빌드 후 `npm`에 publish

**Storybook**의 경우 `build-storybook` 이라는 커맨드를 제공하며, 이를 통해 <u>static web 형태로 빌드</u>할 수 있다. CI를 이용하고 있다면 push가 이루어 질 때마다 Storybook을 빌드하고, output 파일(html, js, css)을 배포하여 팀원들에게 그 링크를 공유할 수 있을 것이다. 우리는 `gitlab-ci`를 통해 위 작업을 자동화하였다.


<p class="center">
  <img src="/attachs/sc-st-on-react/dist-storybook.png" alt="dist-storybook" width="250" height="212">
  <span class="caption">build-storybook의 output 파일</span>
</p>

**컴포넌트**의 경우 `npm`에 publish 하여 다른 프로젝트에서 이용할 수 있도록 만들기로 하였다. 모든 코드는 TypeScript로 작성했는데, TypeScript를 사용하지 않는 환경도 지원하기 위해 먼저 `js` + `d.ts`로 컴파일을 해주어야 한다. 또 컴포넌트를 활용하는 타 프로젝트는 스토리 파일이 필요하지 않으므로 스토리 파일들은 이 경우에 빌드 되지 않도록 해주어야 한다.

주의할 점은 webpack 등을 이용하여 <u>standalone한 코드로 배포하지 않았기에</u> dependency를 신경 써서 관리해야 한다는 점이다. *styled-components*와 같은 라이브러리는 컴포넌트 프로젝트를 설치할 때 함께 설치되어야 하기에 package.json에서 `dependencies`에 포함되어야 하며, *Storybook 및 관련 라이브러리*는 같이 설치가 될 필요가 없으므로 `devDependencies`에 기술되어야 할 것이다.



```json
{
  ...,
  "main": "dist/index.js",
  "types": "dist/index.d.ts",
  "scripts": {
    "storybook": "start-storybook",
    "lint": "tslint -p . -c tslint.json",
    "build": "rm -rf dist && tsc -d",
    "build-storybook": "build-storybook -c .storybook -o dist-storybook",
    "deploy-storybook": "./scripts/deploy"
  },
  "devDependencies": {
    ...,
    "@storybook/addon-knobs": "^5.0.11",
    "@storybook/react": "^5.0.6",
    "@types/react": "^16.8.13",
    "@types/storybook__addon-knobs": "^5.0.0",
    "@types/styled-components": "^4.1.14",
  },
  "dependencies": {
    "react": "^16.8.6",
    "react-dom": "^16.8.6",
    "styled-components": "^4.2.0"
  }
}
```



컴포넌트가 수정되고 push가 이루어지면 Storybook이 새로이 빌드 되어 내부 서버에 배포된다. 이후 팀원들이 배포된 Storybook을 보고 QA 작업을 거친 후, 안정화가 되면 npm에 컴포넌트를 새로운 버전으로 publish한다. 제품에서는 새롭게 업데이트된 컴포넌트를 load하여 development stage에 올릴 것이며, 제품 코드 또한 안정화되면 production에 반영될 것이다.

이와 같은 작업을 진행하는 것이 초기에는 꽤 큰 비용으로 작용하기는 하지만, **장기적**으로 생각해보면 **가치 있는** 작업이라 생각한다. 컴포넌트의 안정성을 높이고 팀원 간의 커뮤니케이션 비용을 낮추는 장점 이외에도, 같은 컴포넌트를 사용하는 다른 프로젝트를 진행하거나 UI의 대규모 개편을 할 때에도 큰 도움이 될 것을 생각하면 해볼 만한 일일 것이다.



