# 2022.07.11 TIL

## Form태그 onClick이벤트로 데이터 보내기

**api.js파일**

```jsx
export async function setQuestion(request) {
  try {
    const apiToken = getApiToken();
    let URL = "https://onecollection.co.kr/api/question/" + apiToken;
    return await fetch(URL, {
      method: "POST",
      body: request,
    })
      .then(function (response) {
        return response.json();
      })
      .then(function (response) {
        console.log(
          "code : " + response["code"] + ", msg : " + response["msg"]
        );
        return response;
      })
      .catch((error) => console.log("error:", error));
  } catch (error) {
    console.log(error);
    return 0;
  }
}
```


```jsx
const clickEvent = () => {
  const form = document.getElementById("formData");
  const formData = new FormData(form);
  **api**.setQuestion(formData).then(function (response) {
    console.log(response);
  });
};
```

form태그에 form id=”formData” 아이디값 지정 해주고 

submit 버튼 누르면 위 onClick이벤트 발생 함수를 적용시킨다.

