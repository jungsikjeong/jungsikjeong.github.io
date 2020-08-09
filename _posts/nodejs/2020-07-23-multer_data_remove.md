---
layout: post
title: nodejs 파일 업로드 - multer 이미지 지우기 
category: nodejs
tags: [nodejs]
comments: true
---

# nodejs 파일 업로드 - multer 이미지 지우기 

> 서버에 저장된 이미지를 지우는 것이아닌, 서버에 올라가기전 미리보기 이미지 UI에있는 이미지를 지우는 것입니다!!

## 클릭시 이미지 지우기

- indexOf를 활용해 각각의 index를 가져온다.

- splice를 활용해준다.
  - filter를 사용해도 될듯하다.

```javascript
  const deleteHandle = (image) => {
    const currentIndex = Images.indexOf(image);
    // console.log(currentIndex);
    let newImages = [...Images];
    newImages.splice(currentIndex, 1);

    setImages(newImages); 
    // 내가 클릭한 이미지의 index 번호~1까지 지워주겠다는뜻,
    // Ex) index 번호 0을 클릭했다면 0부터1까지 지우는거니, 하나만 지움
    // Ex2) index 번호 2를 클릭했다면 2부터3까지 지우는거니, 하남나 지움
  };
```
## 전체 코드
- Front

```javascript
import React, { useState } from 'react';
import Dropzone from 'react-dropzone';
import { Icon } from 'antd';
import axios from 'axios';

const FileUpload = () => {
  // 업로드할 이미지들을 담는 용도
  const [Images, setImages] = useState([]);

  const dropHandle = async (files) => {
    let formData = new FormData();

    const config = {
      header: { 'content-type': 'multipart/form-data' },
    };
    formData.append('file', files[0]);

    axios.post('/api/product/image', formData, config).then((response) => {
      if (response.data.success) {
        // console.log(response.data);
        setImages([...Images, response.data.filePath]);
      } else {
        alert('파일을 저장하는데 실패했습니다.');
        console.log(response.data.err);
      }
    });
  };

  const deleteHandle = (image) => {
    const currentIndex = Images.indexOf(image);
    // console.log(currentIndex);
    let newImages = [...Images];
    newImages.splice(currentIndex, 1);

    setImages(newImages); 
    // 내가 클릭한 이미지의 index 번호~1까지 지워주겠다는뜻,
    // Ex) index 번호 0을 클릭했다면 0부터1까지 지우는거니, 하나만 지움
    // Ex2) index 번호 2를 클릭했다면 2부터3까지 지우는거니, 하남나 지움
  };

  return (
    <div style={{ display: 'flex', justifyContent: 'space-between' }}>
      <Dropzone onDrop={dropHandle}>
        {({ getRootProps, getInputProps }) => (
          <div
            style={{
              width: 300,
              height: 240,
              border: '1px solid lightgray',
              display: 'flex',
              alignItems: 'center',
              justifyContent: 'center',
            }}
            {...getRootProps()}
          >
            <input {...getInputProps()} />
            <Icon type='plus' style={{ fontSize: '3rem' }} />
          </div>
        )}
      </Dropzone>

      {/* 이미지를 뿌려주는 UI */}
      <div
        style={{
          display: 'flex',
          width: '350px',
          height: '240px',
          overflowX: 'scroll',
        }}
      >
        {Images.map((image, index) => (
          <div onClick={() => deleteHandle(image)} key={index}>
            <img
              style={{ minWidth: '300px', width: '300px', height: '240px' }}
              src={`http://localhost:5000/${image}`}
            />
          </div>
        ))}
      </div>
    </div>
  );
};

export default FileUpload;
```

### 결과물
<center>
 <figure>
<img src="https://media.vlpt.us/images/wndtlr1024/post/968561e9-5ab7-4eac-883b-55ff6e20e5e6/GIF%202020-07-23%20%EC%98%A4%ED%9B%84%209-35-05.gif" alt="views" />
 <figcaption>클릭시, 미리보기 이미지를 삭제해주는 모습.</figcaption>
 </figure>
 </center>