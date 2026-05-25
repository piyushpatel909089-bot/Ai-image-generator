<!DOCTYPE html>
<html>
<head>
  <title>AI Image Generator</title>

  <style>
    body{
      background:#111;
      color:white;
      font-family:Arial;
      text-align:center;
      padding:20px;
    }

    input{
      width:80%;
      padding:15px;
      border:none;
      border-radius:10px;
      font-size:18px;
    }

    button{
      margin-top:15px;
      padding:12px 25px;
      font-size:18px;
      border:none;
      border-radius:10px;
      background:#00ff99;
      cursor:pointer;
    }

    img{
      margin-top:20px;
      width:90%;
      max-width:500px;
      border-radius:15px;
    }
  </style>
</head>

<body>

<h1>AI Image Generator</h1>

<input
id="prompt"
placeholder="Enter image prompt"
/>

<br>

<button onclick="generateImage()">
Generate
</button>

<br>

<img id="image">

<script>

async function generateImage(){

const prompt =
document.getElementById("prompt").value;

const response = await fetch(
"https://api-inference.huggingface.co/models/stabilityai/stable-diffusion-2",
{
method:"POST",

headers:{
"Authorization":"Bearer YOUR_API_KEY",
"Content-Type":"application/json"
},

body:JSON.stringify({
inputs:prompt
})
}
);

const blob = await response.blob();

document.getElementById("image").src =
URL.createObjectURL(blob);

}

</script>

</body>
</html>
