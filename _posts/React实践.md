---
layout: post
title: "React实践"
subtitle: ''
author: "WangChiech"
header-style: text
tags:
  - 前端框架
---



## style

### `styled-components` 

>  使组件内style只对自己生效

1. `yarn add styled-components` 

2. 将.css文件名修改为.js文件名，还是直接 `import './... .js'` 引入

   ```javascript
   // style.js
   import { injectGlobal } from 'styled-components
   import styled from 'styled-components
   import logoPic from '../../statics/logo.png
   
   injectGlobal`
   	body {
   		margin: 0;
   		padding: 0;
   		...
   	}
   `
   export const HeaderWrapper = styled.div`
   	height: 56px;
   	background: red;
   `
   export const Logo = styled.a.attrs({href: '/'})`
   	display: inline-block;
   	position: absolute;
   	top: 0
   	left: 0;
   	background: url(${logoPic});
   `
   export const Nav = styled.div`
   	width: 960px'
   	.iconfont { // 里面的具有onfont类名的样式设置
   		color: red;
   	}
   `
   export const NavItem = styled.div`
   	line-height: 24px;
   	&.left { // 个性样式
   		float: left;
   	}
   	&.right
   		float: right
   	}
   	&.active
   		color: #eee;
   	}
   `
   ```

   ```js
   // header.js
   import React, { Component } from 'react'
   import { HeaderWrapper, Logo, Nav, NavItem } from './styled'
   
   class Header extends Component {
       render() {
           <HeaderWrapper>
               <Logo href='/'>
               <Nav>
                   <NavItem className="left active">首页</NavItem>
                   <NavItem className="right active">登录</NavItem>
          		</Nav>
           
           </HeaderWrapper>
       }
   }
   
   export default Header
   ```

   