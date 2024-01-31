cp.5 multer로 서버에 비디오 저장하기

---

서버에 비디오를 저장하는 기능! = 0. ondrop func 만들기  


서버에다가 request를 보낼건데, axios를 사용할 거기 때문에, axios 라이브러를 보내고 받고 한다.
(React에서 Axios.post로 "/api/users/uploadfiles를 보내기 때문)

오류가 생기기 때문에, 헤더에다가 content를 해줘야지만 오류가 생기지 않는다.


```
  const onDrop = (file) => {
        let formData = new FormData;
        const config = {
            header: {'content-type':'multipart/form-data'}
        }
        formData.append("file", files[0])

        Axios.post('/api/')
  }
```


```
                <Dropzone
                onDrop={onDrop}
                multiple
                maxSize>
                {({ getRootProps, getInputProps }) => (
                   <div style={{ width: '300px', height: '240px', border: '1px solid lightgray',
                   alignItems: 'center', justifyContent: 'center' }} {...getRootProps()}>
                                <input {...getInputProps()} />
                                <Icon type="plus" style={{ fontSize: '3rem' }} />
                            </div>
                )}
```


multiple은 여러개 할건지를 정한다. 



```
        Axios.post('/api/video/uploadfiles', formData, config)
        .then(response=>{
            if (response.data.success){

            }else {
                alert('비디오 업로드를 실패했습니다'
                )
            }
  })
```

이 기능을 통해서, 비디오 성공 if문 작성. 하지만 이 상태로는 라우터가 되지 않으니, 라우터를 설정해줘야한다.

```
const express = require('express');
const router = express.Router();
const { Video } = require("../models/Video");

const { auth } = require("../middleware/auth");

//=================================
//             Video
//=================================
```
server - routes에 video.js 파일을 생성한다. (기존에 있던 route - user.js 파일을 복사하여 수정해서 사용한다)


```
app.use('/api/users', require('./routes/users'));
app.use('/api/video', require('./routes/video'));
```

index.js에서 해당 내용을 video를 추가한다.  그다음에 video에서 post할대 index에 있는걸 읽은 다음에 video.js로 불러오기 때문이다 .

```

router.post('/uploadfiles', (req, res) => {
    // 비디오를 서버에 저장한다.
})
```
videojs에서 이렇게 입력하면 된다. 즉. index에서 저렇게 경로를 입력했기 때문에,  
router.post('/api/video/uploadfiles', (req, res) => {
    // 비디오를 서버에 저장한다.
})


이런식으로 작성 안해도 된다!

1. 노드 서버 파일을 저장하기 위해, dependency 다운로드 하기 
----

```
npm install multer --save
```

서버 디렉토리에 저장한다!

디펜더시를 다운 받고 나서는 꼭 서버를 재가동해준다. 


```
//storage multer config
let storage = multer.diskStorage({
    destination: (req, file, cb) => {
      cb(null, "uploads/"); 
      //uploads라는 폴더를 생성해야함!
    },
    filename: (req, file, cb) => {
      //파일이름 -> 현재시간_파일이름
      cb(null, `${Date.now()}_${file.originalname}`);
    },
    fileFilter: (req, file, cb) => {
      const ext = path.extname(file.originalname);
        //파일확장자 mp4만허용      
      if (ext !== ".mp4") {
        return cb(res.status(400).end("only mp4 is allowd"), false);
      }
      cb(null, true);
    },
  });
```

video js에 위와 같이 입력한다. 


```
//=================================
//             Video
//=================================


router.post('/uploadfiles', (req, res) => {
    // 비디오를 서버에 저장한다.

    UploadVideoPage(req, res, err => {
        if(err) {
            return res.json({success:false, err})
        }
    })
})
```

upload를 만들었으니, 위 내용을 적어준다. 만약 false가 발생한다면 에러메시지를 출력한다. 

```
        Axios.post('/api/video/uploadfiles', formData, config)
        .then(response=>{
            if (response.data.success){

            }else {
                alert('비디오 업로드를 실패했습니다'
                )
            }
```

위 내용이, uploadvideopage.js에 있는 위 코드와 연결되어 있다

```
router.post('/uploadfiles', (req, res) => {
    // 비디오를 서버에 저장한다.

    upload(req, res, err => {
        if(err) {
            return res.json({success:false, err})
        }
        // rse.req~path는 upload path를 보내는 역할을 한다.
        return res.json({success:true, url: res.req.file.path, fileName: res.req.file.path })
    })
})
```

```
        Axios.post('/api/video/uploadfiles', formData, config)
        .then(response=>{
            if (response.data.success){
                console.log(response.data)
            }else {
                alert('비디오 업로드를 실패했습니다'
                )
            }
  })}
```
으로 수정!







오류발생
---

  Line 51:33:  'files' is not defined  no-undef
  Line 53:9:   'Axios' is not defined  no-undef

Search for the keywords to learn more about each error.


axio는 import 처리함. 
files...는


```
  const onDrop = (file) => {
        let formData = new FormData;
        const config = {
            header: {'content-type':'multipart/form-data'}
        }
        formData.append("file", files[0])

        Axios.post('/api/video/uploadfiles', formData, config)
        .then(response=>{
            if (response.data.success){
                console.log(response.data)
            }else {
                alert('비디오 업로드를 실패했습니다'
                )
            }
  })}
```

파라미터 오류로 

```
  const onDrop = (files) => {
        let formData = new FormData;
        const config = {

//생략
```

으로 수정처리.


TypeError: Cannot read properties of undefined (reading 'prototype')


```
import { response } from 'express';
```

입력하지도 않았던 import가 자동으로 입력되어 있어서 삭제처리했다.





createError.js:16 
 Uncaught (in promise) Error: Request failed with status code 504
    at createError (createError.js:16:1)
    at settle (settle.js:17:1)
    at XMLHttpRequest.handleLoad (xhr.js:61:1)
createError	@	createError.js:16
settle	@	settle.js:17
handleLoad	@	xhr.js:61
...
onDrop @uploadvideopage.js:53

이어서 53줄 확인

터미널내 오류
Error: Cannot find module 'multer'

 npm install --save multer

재설치!

npm cache verify

code EEXIST 
npm ERR! Refusing to delete

-> which.cmd 삭제 후 multer 재설치

해도 안되서 우선 보류.