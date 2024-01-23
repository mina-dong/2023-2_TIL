# ch. 3
---
upload page 만들기
---
1.  nodemon 를 이용해서 서버를 가동한다. 클라이언트 부분을 가동하기 위한 내용이 package.json에 입력되어 있으며, 프론트 서버를 함께 가동할 수 있는 환경을 제공하고 있다.  

2. redux extension 
이사람이 관리자인지, 인증받았는지 등을 확인할 수 있다. 
> 새로고침해야지 활성화됨. 

3.  VSC 익스텐션 중 ES7+ React/Redux/React-Native snippets 
js할때 rfce를 입력하면 기본 설정을 입력할 수 있다 = 단축키  

[componets] - [views] 에 videoup~page 폴더 생성 및 하위 videoup~.js 파일생성. 
```
import React from 'react'

function VideoUploadPage() {
  return (
    <div>VideoUploadPage</div>
  )
}

export default VideoUploadPage
```

4. f1 -> reload window를 통해 새로고침 할 수 있음. 

---
upload pagge route 만들기
---

1. app.js 에 들어가서 
import VideoUploadPage from "./views/VideoUploadPage/VideoUploadPage.js"; 추가적으로 입력하고

```
//null   Anyone Can go inside
//true   only logged in user can go inside
//false  logged in user can't go inside

function App() {
  return (
    <Suspense fallback={(<div>Loading...</div>)}>
      <NavBar />
      <div style={{ paddingTop: '69px', minHeight: 'calc(100vh - 80px)' }}>
        <Switch>
          <Route exact path="/" component={Auth(LandingPage, null)} />
          <Route exact path="/login" component={Auth(LoginPage, false)} />
          <Route exact path="/register" component={Auth(RegisterPage, false)} />
          <Route exact path="/register" component={Auth(RegisterPage, false)} />

        </Switch>
      </div>
      <Footer />
    </Suspense>
  );
}
```

에 route 설정을 한다. 

//null   Anyone Can go inside
//true   only logged in user can go inside
//false  logged in user can't go inside

null은 누구나 들어갈 수 있고, true는 로그인한 사람만 들어갈 수 있는 등, 권한을 설정할 수 있다. 

---
upload page header tab만들기
---
1. rightmenu.js
```
 if (user.userData && !user.userData.isAuth) {
    return (
      <Menu mode={props.mode}>
        <Menu.Item key="mail">
          <a href="/login">Signin</a>
        </Menu.Item>
        <Menu.Item key="app">
          <a href="/register">Signup</a>
        </Menu.Item>
      </Menu>
    )
  } else {
    return (

      <Menu mode={props.mode}>
         <Menu.Item key="upload">
          <a href="/video/upload">Video</a>
        </Menu.Item>

        <Menu.Item key="logout">
          <a onClick={logoutHandler}>Logout</a>
        </Menu.Item>
      </Menu>
    )
  }
}
```

위는 로그인하기전에,
아래는 로그인 이후의 값을 return함. 
---
videoform 만들기
---
1. 앤드디자인
import { Typography, Button,Form,message,Input,Icon } from 'antd'

```
import React from 'react'
import { Typography, Button,Form, message,Input,Icon } from 'antd';

const { TextArea} = Input;
const { Title} = Typography;

function UploadVideoPage() {
  return (
    <div style={{maxWidth:'700px', margin:'2rem auto'}}>
        <div style={{textAlign:'center', marginBottom:'2rem'}}>
            <Title level={2}>upload video</Title>
        </div>

        <Form onSubmit>
            <div style={{display:'flex', justifyContent:'space-between'}}>
                {/* drop zone */}
                {/* Thumbnail */}
                <div>
                    <img src alt/>
                </div>
            </div>
    <br/>
    <br/>
    <label>Title</label>
    <Input
        onChange
        value
    />
    <br/>
    <br/>
    <label>Description</label>
    <TextArea
        onChange
        value
    />
    <br/>
    <br/>

    <select onChange>
        <option key value></option>
    </select>

    <select onChange>
        <option key value></option>
    </select>

    <Button type="primary" size="large" onClick>
        SUBMIT
    </Button>

        </Form>

        </div>
  )
}

export default UploadVideoPage
```

2. 클라이언트에 디펜더시 설치하기 
cd client
npm install react-dropzone --save


설치이후 다시 루트로 돌아가서 cd .. 
npm run dev 실행. 

```
import React from 'react'
import { Typography, Button,Form, message,Input,Icon } from 'antd';
import Dropzone from 'react-dropzone'

const { TextArea} = Input;
const { Title} = Typography;

function UploadVideoPage() {
  return (
    <div style={{maxWidth:'700px', margin:'2rem auto'}}>
        <div style={{textAlign:'center', marginBottom:'2rem'}}>
            <Title level={2}>upload video</Title>
        </div>

        <Form onSubmit>
            <div style={{display:'flex', justifyContent:'space-between'}}>
                {/* drop zone */}
                <Dropzone
                onDrop
                multiple
                maxSize>
                {({ getRootProps, getInputProps }) => (
                   <div style={{ width: '300px', height: '240px', border: '1px solid lightgray',
                   alignItems: 'center', justifyContent: 'center' }} {...getRootProps()}>
                                <input {...getInputProps()} />
                                <Icon type="plus" style={{ fontSize: '3rem' }} />
                            </div>
                )}
                </Dropzone>

                {/* Thumbnail */}
                <div>
                    <img src alt/>
                </div>
            </div>
    <br/>
    <br/>
    <label>Title</label>
    <Input
        onChange
        value
    />
    <br/>
    <br/>
    <label>Description</label>
    <TextArea
        onChange
        value
    />
    <br/>
    <br/>

    <select onChange>
        <option key value></option>
    </select>

    <select onChange>
        <option key value></option>
    </select>

    <Button type="primary" size="large" onClick>
        SUBMIT
    </Button>

        </Form>

        </div>
  )
}

export default UploadVideoPage
```