cp17~18 mongoDB
---
...
그냥 직접 폴더 경로로 들어가서 mongo.exe 파일을 실행시켜주면 되는듯하다.
그러면 바로 cmd? 켜지고 mongodb shell이라고 표시됨. 

```
show dbs
```
라고 입력하면 admin, config, local 에서 얼마나 사용하고 있는지를 확인할 수 있다.

```
use express
```
데이터 베이스 중에 지정해주는 명령어다. 그래서 이걸 입력하면 express 를 데이터 베이스로 사용한다는 것을 의미한다.
다시 show dbs를 입력하면, express는 표시되지 않은 것을 확인할 수 있는데.  
안에 아무런 데이터가 없어서 그렇다. 


```
db.createCollection('writings')
```
을 입력하고, show dbs를 입력하면   
express가 목록에 차지하는것을 확인할 수 있다.  

```
show collections
```
라고입력하면 콜렉션들 리스트를 확인할 수 있다. 
이 안에 다큐먼트를 만들어볼건데,   
직접 데이터 베이스 않에 글을 작성해볼수도 있다. 	

```
db.writings.insert({"title":"title1","date":"2024-02-05"})
db.writings.insert([{"title":"title1","date":"2024-02-05"},{"title":"title2","date":"2024-02-06"}])

```
이런식으로 직접 추가할 수 있다 . 2개이상할때는 bulk, []중괄호를 입력해야한다. 안그러면 입력하다가 오류난다..   

```
db.colletionname.find()
db.colletionname.find().pretty()


```

db.writings.find() 를 입력하면 된다. 보기좋게 출력하려면, pretty()를 덧붙여준다

데이터베이스이기 때문에 각자 고유한 id를 가지게 된다.  





```
app.post('/write', async (req, res) => {
    const title = req.body.title;
    const contents = req.body.contents;
    const date = req.body.date;

    // 데이터 저장
    // data/writing.json 안에 글 내용 저장.
    //readfilesync를 이용함. 노드제이에스는 비동기적인데, 다음 메시지를 실행할 수 있게끔.
    const fileData = fs.readFileSync(filePath);
    //console.log(fileData);

    const writings = JSON.parse(fileData)
    // console.log(writing);

    //request 데이터 저장
    writings.push({
         'title':title,
         'content':contents,
         'date':date
     });

    //data/writing.json에 저장하기
    fs.writeFileSync(filePath, JSON.stringify(writings));

   res.render('detail', { 'detail': { title: title, contents: contents, date: date } });
});
```

```
app.post('/write', async (req, res) => {
    const title = req.body.title;
    const contents = req.body.contents;

    //mongodb에 저장
    const writing = new Writing({
        title:title,
        contents:contents
    })
    const result = await writing.save().then(() =>{
        console.log('Success')
        res.render('detail', { title: title, contents: contents});
    }).catch((err) => {
        console.error(err)
        res.render('write')
    })
});
```
await에 이후가 처리가 되어야 전체적으로 완료가 된다. 이 세이브가 전송이 된다면,  관련 로그를,  오류가 발생한다면 에러를. 
글작성 페이지에 작성하면 콘솔창에 success 라는 로그를 확인할 수 있다.


```
app.get('/', async (req, res) => {
    const fileData = readFileSync(filePath);
    const writings = JSON.parse(fileData);


    res.render('main', {list:writings});
});
```
이런식으로 json을 받아오는 역할을 했다면, 


```
const Writing = mongoose.model('writing', WritingSchema);

app.get('/', async (req, res) => {
    let writings = await Writing.find({})

    res.render('main', {list:writings});
});
```

데이터베이스에 연결해야하기 때문에 라이팅즈로 가져오고. 
find에 아무값도 입력하지 않으면 모든 값을 가져오고,
값을 가져와야하기때문에 let이라고 설정함. 

```
                        <td><a href="/detail/{{}}">{{writing.title}}</a></td>

```

main에서 위와같이 수정. 고유한아이디 

```
app.get('/detail/:id', async (req, res) => {
    const id = req.params.id;

    const detail = await Writing.findOne({_id:id}).then((result)=>{
        res.render('detail',{'detail':detail})
    }).catch((err) =>{
        console.error(err)
    })
    //res.render('detail');
})
```

모든 도큐멘트는 고유의 값을 가지게 되는데, 이 값은 ObejecID로 이 값을 가져오려면 위와같이 작성.


```
<p>글 내용: {{ detail.contents }}</p>
```
detailhtml에서 위와같이 수정. 
다시 메인페이지로 돌아것 보면, 해당 페이지를 아디값을 가진 페이지를 상세하게 보여줌.  


**오류발생*
템플릿엔진 어쩌구 오류.... 검색해보니 강의 중 내용이 빠진것 같다.  
ref: https://www.inflearn.com/chats/989331/%EB%94%94%ED%85%8C%EC%9D%BC-%EB%A9%94%EC%9D%B8%ED%8E%98%EC%9D%B4%EC%A7%80%EC%97%90%EC%84%9C-%EC%83%81%EC%84%B8%ED%8E%98%EC%9D%B4%EC%A7%80%EB%A1%9C-%EA%B0%80%EB%8A%94-%EB%A7%81%ED%81%AC-%EB%B6%80%EB%B6%84

```
                        <td><a href="/detail/{{}}">{{writing.title}}</a></td>

```

```
                        <td><a href="/detail/{{writing._id}}">{{writing.title}}</a></td>

```

라고 수정했다. 


**오류발생**
ref: https://www.inflearn.com/questions/1012723/%EC%83%81%EC%84%B8-%ED%8E%98%EC%9D%B4%EC%A7%80%EC%97%90-%EB%82%B4%EC%9A%A9%EC%9D%B4-%EB%B3%B4%EC%9D%B4%EC%A7%80-%EC%95%8A%EC%9D%8C-%EB%AC%B8%EC%9D%98-%ED%99%95%EC%9D%B8-%EA%B3%B5%EC%9C%A0


cp.20 삭제기능
---

디비에 연결되는 작업이기때문에 async를 사용함. 

위의 오류발생에 참고하면 코드가 아예 달라졌음. 그걸 보고 참고해서 작성함. 

```
app.post('/delete/:id', async (req, res) => {
    const id = req.params.id;

    let no_error = false
    let detail = null
    await Writing.deleteOne({_id: id}).then((result)=>{
        detail = result
        no_error = true
        res.render('detail', {'detail':detail})

    }).catch((err)=>{
        console.error(err)
    })
})
```

이렇게 적엇고, get에서 post사용 findone에서 deleteone을 사용했다. 


21챕터의 내용은 부트스트랩을 이용해서 테이블 정렬 및 정리여서 여기에서 강의를 마무리한다.  