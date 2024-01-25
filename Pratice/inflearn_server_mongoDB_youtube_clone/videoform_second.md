# ch. 4
---
value를 저장하는 status 
---
한꺼번에 서버에 값을 전달할 수 있다.

import React, { useState } from 'react'
usestate 를 입력하면 const [state, setstate] = usestate(initialState) 가 자동입력되는데 이걸 리액트 훅이라고 한다. 
-> 구버전이여서 usestatesnitpet 이 이 기능에 해당한다. 

```
    <label>Title</label>
    <Input
        onChange
        value ={VideoTitle}
    />
```


```
  const [VideoTitle, setVideoTitle] = useState("")
  const [Description, setDescription] = useState("")
  const [first, setfirst] = useState(0)
```

문자열은 "" 프라이빗으로 하려면 0, 아니면 = 퍼블릭이면 1



```
const Private = [ 
    {value:0, label:"private"},
    {value:1, label:"public"}
]
```

이렇게 작성하고 

```
    <select onChange>
       {Private.map((item,index) =>(
        <option key={index} value={item.value}>  {item.label} </option>
       ))}
    </select>
```
        <option key value></option>
        <option key value></option>

이걸 이렇게 두개 입력하는 방법도 있지만, 저렇게 값을 부여하는 형식도 있다. 
map을 사용하려면 항상 key가 있어야지 에러가 안생긴다. 


=> 오류발생. 
" TypeError: private.map is not a function "

중간중간저장하면서 비교하고 있는데, 알고보니 내부에도 private라고 선언한게 있는데(두 개다 동일한 이름을 가지고 있음) 그걸로 map()을 실행하려고 보니 생긴 오류같다. 

즉 변수명을 수정해서 해결했다. 


```
    <TextArea
        onChange
        value={Description}
    />
```

여기서 텍스트 입력하는 칸은 있는데 입력되지는 않는데, onchnage에 아무런 속성도 부여되지 않았기 때문이다. 


```
  const onChangeTitleChang = (e) => {
    setVideoTitle(e.currentTarget.value)
  }

  const onChangeDescriptionChang = (e) => {
    setDescription(e.currentTarget.value)
  }


//중략

    <label>Title</label>
    <Input
        onChange={onChangeTitleChang}
        value ={VideoTitle}
    />
    <br/>
    <br/>
    <label>Description</label>
    <TextArea
        onChange={onChangeDescriptionChang}
        value={Description}
    />
    <br/>
    <br/>
```

e는 이벤트를 의미한다. 



---
전체코드
---

```
import React, { useState } from 'react'
import { Typography, Button,Form, message,Input,Icon } from 'antd';
import Dropzone from 'react-dropzone'

const { TextArea} = Input;
const { Title} = Typography;
const PrivateOptions = [ 
    {value:0, label:"private"},
    {value:1, label:"public"}
]

const CategoryOptions = [ 
    {value:0, label:"film&animation"},
    {value:1, label:"autos & vehicles"},
    {value:2, label:"autos & vehicles"},
    {value:3, label:"autos & vehicles"},
    {value:4, label:"autos & vehicles"},

]


function UploadVideoPage() {

  const [VideoTitle, setVideoTitle] = useState("")
  const [Description, setDescription] = useState("")
  const [Private, setPrivate] = useState(0)
  const [Category, setCategory] = useState("film&animation")

  const onChangeTitleChang = (e) => {
    setVideoTitle(e.currentTarget.value)
  }

  const onChangeDescriptionChang = (e) => {
    setDescription(e.currentTarget.value)
  }

  const onPrivateChange = (e) => {
    setPrivate(e.currentTarget.value)
  }

  const onCategoryChange = (e) => {
    setCategory(e.currentTarget.value)
  }

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
        onChange={onChangeTitleChang}
        value ={VideoTitle}
    />
    <br/>
    <br/>
    <label>Description</label>
    <TextArea
        onChange={onChangeDescriptionChang}
        value={Description}
    />
    <br/>
    <br/>

    <select onChange={onPrivateChange}>
       {PrivateOptions.map((item,index) =>(
        <option key={index} value={item.value}>  {item.label} </option>
       ))}
    </select>

    <br/>
    <br/>
    <select onChange={onCategoryChange}>
       {CategoryOptions.map((item,index) =>(
        <option key={index} value={item.value}>  {item.label} </option>
       ))}
    </select>

    <br/>
    <br/>

    <Button type="primary" size="large" onClick>
        SUBMIT
    </Button>

        </Form>

        </div>
  )
}

export default UploadVideoPage
```