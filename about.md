---
layout: page
title: Sobre mí
---
<style>
.profile-pic {
  display: false;
  position: absolute;
  margin: false;
  top: -90px;
  //left: 50%;
  right: false;
  bottom: false;
  -webkit-transform: translateX(-50%);
          transform: translateX(-50%);
  height: 180px;
  width: 180px;
  border: 10px solid #008A3C;
  border-radius: 100%;
  background: url("https://sessionize.com/image?f=c79339ef43e8a87e01d46f3489e5f5ba,0,0,False,False,2c-e253-4013-8264-7fe756989f4c.99f601ce-9a02-4772-a3a7-402088e7a344.png"
            ) center no-repeat;
  background-size: cover;
}
.profile-name-container {
  margin: 0 auto 10px;
  padding: 10px;
  text-align: center;
}
.user-name {
  font-size: 24px;
  font-weight: 400;
  line-height: 30px;
  margin-bottom: 12px;
}
.user-desc {
  color: #999;
}
.profile-card-stats {
  height: 75px;
  padding: 10px 0px;
  text-align: center;
  overflow: hidden;
}
.profile-stat {
  height: 100%;
  width: 33.3333%;
}
.profile-stat:after {
  color: #999;
}
.works::after {
  content: "works";
}
.followers::after {
  content: "followers";
}
.following::after {
  content: "following";
}
.image {
  width: 240px;
  height: 200px;
  cursor: pointer;
  margin: 0 20px 40px;
  overflow: hidden;
  border-radius: 5px;
  border: 10px solid #fff;
  box-shadow: 0 2px 6px -2px rgba(0,0,0,0.26);
  background-color: rgba(0,0,0,0.4);
  background-size: cover !important;
  -webkit-transition: 0.2s cubic-bezier(0.5, 0, 0.2, 1);
  transition: 0.2s cubic-bezier(0.5, 0, 0.2, 1);
}
.image:hover {
  -webkit-transform: scale(1.06);
          transform: scale(1.06);
  box-shadow: 0 2px 18px -2px rgba(0,0,0,0.3);
}
.image.hidden {
  height: 0;
  width: 0px;
  margin: 0px;
  border: 0px solid #fff;
}

@media screen and (max-width: 1300px) {
  .container {
    max-width: 843px;
  }
  .overlay-card {
    max-width: 803px;
    padding: 0;
  }
  .overlay-image {
    height: 68%;
    width: 100%;
  }
  .overlay-desc {
    width: 100%;
    height: 32%;
    margin: 0;
    padding: 20px 40px;
  }
}
@media screen and (max-width: 1000px) {
  .overlay-card {
    max-width: 522px;
    min-width: 310px;
  }
  .overlay-image {
    width: 100%;
    height: 55%;
    max-height: 1000px;
    margin: 0;
  }
  .post-image {
    width: 396px;
    height: 330px;
    border: 0px solid #fff;
    box-shadow: 0 0 0 rgba(0,0,0,0);
    background-size: contain !important;
  }
  .overlay-desc {
    width: 100%;
    height: 45%;
    padding: 20px;
  }
  
  .menu-background {
    left: 8%;
  }
  .menu-card {
    left: 2px;
    height: 360px;
  }
  .menu-content .sub-nav-links {
    height: 164px;
    border-bottom: 1px solid #ccc;
  }
}
@media screen and (max-width: 630px) {
  .image {
    width: calc(100% - 40px);
    height: 0px;
    padding-bottom: 60%;
  }
  .menu-content .sign-links {
    height: 64px;
    border-top: 1px solid #ccc;
  }
  .menu-card {
    height: 425px;
  }
  .sign-div {
    width: 0px;
  }
  .nav-search.active {
    -webkit-transition: 0.3s cubic-bezier(0.75, 0, 0.2, 1);
    transition: 0.3s cubic-bezier(0.75, 0, 0.2, 1);
  }
}
@media screen and (max-width: 550px) {
  .overlay-card {
    height: 500px;
  }
  .post-image {
    width: 80%;
    max-width: 288px;
    height: 240px;
  }
  .overlay-desc {
    padding: 14px;
  }
  .profile-pic {
    height: 140px;
    width: 140px;
    top: -141px;
    left: 140px;
  }
}
</style>


<div class="rela-block profile-card">
    <div class="profile-pic" id="profile_pic"></div>
    <div class="rela-block profile-name-container">
        <div class="rela-block user-name" id="user_name">J. Rafa Ramón</div>
        <div class="rela-block user-desc" id="user_description">Software Developer Enginner</div>
    </div>
    <div class="rela-block profile-name-stats">
        <p>Mi nombre es Rafa. Actualmente, desarrollo mis labores
        como desarrollador de Software, principalmente en tecnologías .Net con
        Azure.</p>
        <p> Personalmente, me apasiona cualquier cosa que me tenga enfrascado
        un buen rato, que inicialmente, me llame la atención y me frustre y que
        finalmente llegue a entender y poder decir, “esto lo he hecho yo y así
        lo he hecho. Mejorémoslo”. No todo es código, aunque mi profesión es
        mi hobbie.</p> 
        <p>También disfruto caminando, con mis guitarras, la horticultura/jardinería,
        cocinando, leyendo, la música o haciendo algún que otro amigurumi. Con
        este curriculum, no creo que puedas adivinar lo siguiente que aprenderé.</p>
    </div>
</div>