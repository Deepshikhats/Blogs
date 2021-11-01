# Uploading Files using Multer in Express.js

### In this blog file, uploading file using multer in express.js is explained

## What is Multer?
### Multer is a node.js middleware for handling multipart/form-data, which is primarily used for uploading files.

#### So let's start with code.
## Frontend
```
<form action="/profile" method="post" enctype="multipart/form-data">
  <input type="file" name="Uploaded_file" />
</form>
```
#### Here **enctype** attribute specifies how data should be encoded by the browser before sending to the server and **/profile** defines the path of the application.

## Backend
#### In the terminal install multer
```
$ npm install multer
```

```
const multer  = require('multer')

const upload = multer({
  dest : 'images',
  limits : {
    fieldSize : 1000000
  },
  fileFilter(req,file,cb){
    if(!file.originalname.endsWith('.jpeg')){
      return cb(new Error("file must be jpeg format"))
    }
    cb(undefined,true)
  }
})
```
 
> **dest** or **storage** specifies the destination folder. Image will be saved in filename (eg: 4aeddf8e8745e849e1a384fa9430c9e3)  \

> **limits** allows to add limits to uploading files. This is an optional parameter \

>**fileFilter** helps to control which files should be uploaded and which should be skipped. This is also optional.


```
app.post('/upload',upload.single('Uploaded_file'),(req,res) =>{
  res.json({message :'file uploaded'})
  console.log(req.file)
},
  (error,req,res,next) => {
    res.status(400).json({error : error.message})
  }
)
```

### In console 
```
  fieldname: 'Uploaded_file',
  originalname: 'Deepshikha_photo (1).jpg', \
  encoding: '7bit', \
  mimetype: 'image/jpeg', \
  destination: 'images', \
  filename: '4aeddf8e8745e849e1a384fa9430c9e3', \
  path: 'images\\4aeddf8e8745e849e1a384fa9430c9e3', \
  size: 101738
  ```


> **upload.single('Uploaded_file')** :- Accepts only a singlefile with field name 'Uploaded_file'. This fieldname must be same as the name attribute from frontend.

> **req.file** gives full details of uploaded file

## Conclusion

### With multer, we can easily handle single or multiple files in addition to text inputs sent through a form.




