<template>
 <!-- ONE POSTIT API -->
 <form >
  <p>
    <input type="text" v-model = "form.title" placeholder="Titre"/>
    <br/>
    
    <input type="text" v-model = "form.content" placeholder="Content"/>
    <br />
    

    <input class="bouton" type="submit" id="envoyer" v-on:click="put()" value="EDIT this postit"/>
  </p>
</form>



<div  class="widget-notification-postit" > 
    <div class="title-notification-postit">{{list.title}}</div>
	
    <div class="recado-notification-postit">
      {{list.content}}
    </div>
  <RouterLink to="/view"> back</RouterLink>

  </div>

  

</template>


<script> 
// import axios from "axios"
export default {
  data()
  {
    return {
      form:{
        title:'',
        content:''
      },
        list:[]

        
    }
},
mounted()
{
    const id = this.$route.params.id;
    fetch("http://5.135.119.239:3090/notes/"+id)
    .then(response => response.json())
    .then(data => this.list=data.note)
    // console.log(id)
    
  },
    methods:{
      put() {
        const id = this.$route.params.id;
        console.log(id),
        fetch(`http://5.135.119.239:3090/notes/${id}`, {
          method: "PUT",
          headers:{
            "content-type":"application/json",
          },
          body: JSON.stringify( {
            title:this.form.title,
            content:[this.form.content]
            
          })
        });
        this.$toast.success(`Success Edit`);
        setTimeout(this.$toast.clear, 10000);

      }
    }
}
</script>



<style>

/* #by{
  width: 100%;
  color: #888;
  font-size: 13px;
  text-align: center;
} */

/* body {
  color: #888;
text-align : center;
} */

form input {
outline : none;
border : none;
border-bottom : 2px solid darkOrange;
margin : 0 0 50px 0;
width : 250px;
text-align : center;
font-size : 0.9em;
}

form .bouton {
outline : none;
border : 1px solid white;
margin : 15px 0 0 0;
padding : 10px 25px;
font-size : 0.9em;
width: 250px;
color : darkOrange;
border : 2px solid darkOrange;
background-color : white;
transition : all .2s;
}

form .bouton:hover {

color : white;
background-color : darkOrange;
transition : all .2s;
}




/* @import url(https://fonts.googleapis.com/css?family=Gloria+Hallelujah); */

body{
	width:50%;
	margin:auto;
	padding-top:30px;
	padding-bottom:30px;
  background-image: linear-gradient(to right, #fa709a 0%, #fee140 100%);}

/*CHAT*/
.widget-notification-chat{
  word-wrap: break-word;
  position: relative;
  padding: 10px 20px;
  border-radius: 25px;
  clear:both;
  font: 100 13px 'Open Sans', sans-serif;
	background: #dcf8c6; /*cor do balão*/
	color: #1b1b1b; /*cor do texto */
	border-bottom-left-radius: 30px 0px\9;
}
.title-notification-chat{
	font-weight:bold;
	display: inline-block;
}
.date-notification-chat{
	display: inline-block;
}
.date-notification-chat:before{
	content: "- ";
}
.widget-notification-chat:before{
  content: "";
  /* position: absolute; */
  z-index: 2;
  bottom: -2px;
  left: -7px;
  height: 19px;
  border-left: 20px solid #dcf8c6; /*cor do balão*/
  border-bottom-right-radius: 16px 14px;
  -webkit-transform: translate(0, -2px);
  transform: translate(0, -2px);
  border-bottom-right-radius: 15px 0px\9;
  transform: translate(-1px, -2px)\9;
}
.widget-notification-chat:after{
  content: "";
  /* position: absolute; */
  z-index: 2;
  bottom: -2px;
  left: 4px;
  width: 26px;
  height: 20px;
  background: #fff; /*cor de fundo*/
  border-bottom-right-radius: 10px;
  -webkit-transform: translate(-30px, -2px);
  transform: translate(-30px, -2px);
}
/*CHAT*/

/*POSTIT*/
.widget-notification-postit {
  background: #FFF9C4;
  margin: 60px auto;
  padding: 10px;
  box-shadow: 0px 10px 10px rgba(0, 0, 0, 0.2);
  color: #1b1b1b;
}
.title-notification-postit {
	font-family: 'Gloria Hallelujah', cursive;
  margin: -30px auto 10px;
  width: 200px;
  height: 40px;
  background: rgba(255,255,200,0.4);
  -webkit-box-shadow: 0px 1px 3px rgba(0,0,0,0.4);
  -moz-box-shadow: 0px 1px 3px rgba(0,0,0,0.4);
  box-shadow: 0px 1px 3px rgba(0,0,0,0.4);
  text-align: center;
  line-height: 40px;
  font-weight: bold;
  color: #1b1b1b;
	color: #215096;
}
.recado-notification-postit{
	font-family: 'Gloria Hallelujah', cursive;
	margin: 10px;
	font-size: 12px;
  text-align: center;
  margin-bottom: 15px;
  word-wrap: break-word;
	color: #215096;
}
.date-notification-postit{
	font-family: 'Gloria Hallelujah', cursive;
	text-align: right;
	margin:10px;
	color: #215096;
}
/*POSTIT*/

.widget-notification-windows{
  background: #c0c0c0;
  border: 1px solid black;
  border-color: #dfdfdf black black #dfdfdf;
  position: relative;
	padding-bottom: 20px;
}
.widget-notification-windows:before{
	content: "";
  display: block;
  /* position: absolute; */
  left: 0;
  top: 0;
  right: 0;
  bottom: 0;
  border: 1px solid green;
  border-color: white #808080 #808080 white;
}
.widget-notification-windows * {
  cursor: default;
}
.title-notification-windows{
	font-family: "MS Sans-Serif", Tahoma, sans-serif;
  font-size: 12px;
  font-weight: bold;
  background: linear-gradient(to right, #000080, #1084d0);
  /* position: absolute; */
  left: 3px;
  top: 3px;
  right: 3px;
  margin: 0;
  padding: 0;
  line-height: 18px;
  color: white;
  padding-left: 3px;
}
.title-notification-windows .close {
  /* position: absolute; */
  right: 2px;
  top: 2px;
  height: 14px;
  width: 0;
  padding-left: 14px;
  overflow: hidden;
  background: #c0c0c0;
  border: 1px solid green;
  border-color: white black black white;
  box-sizing: border-box;
}
.title-notification-windows .close:before {
  content: "";
  display: block;
  /* position: absolute; */
  left: 0;
  top: 0;
  right: 0;
  bottom: 0;
  border: 1px solid green;
  border-color: #dfdfdf #808080 #808080 #dfdfdf;
}
.title-notification-windows .close:after {
  content: "×";
  position: absolute;
  left: 0;
  width: calc(100%);
  text-align: center;
  top: 50%;
  color: black;
  background: pink;
  line-height: 0;
  margin-top: -1px;
}
.recado-notification-windows{
	margin-left: 20px;
	margin-right: 20px;
	margin-top: 10px;
	font: 14px MS Sans Serif, Arial, sans-serif;
}
.date-notification-windows{
	margin-top: 30px;
	text-align: center;
	font: 14px MS Sans Serif, Arial, sans-serif;
}
</style>


