<template >
  <div class="hello background">
    <h1>TIC TAC TOE</h1>
    <section class="display" id="aQuideJouer">
            
      <p>Player <span id="idSpan" class="display-player playerX">X</span>'s turn</p>
    </section>
    <section class="container">
      <!--             on fait une boucle pour définir les cases -->
      <div v-for="i in 9" v-on:click="()=>cliqueSur(i-1)" class="tile cache">X</div>
     
    </section>
    <section class="controls">
      <button v-on:click="reset()" id="reset">Reset</button>
    </section>
  </div>
</template>

<script setup>

function getRandomInt(max) {
  return Math.floor(Math.random() * max);
}
// on choisit aléatoirement le joueur de départ
let joueurEnCours=getRandomInt(2)
// on définit le tableau contenant les cases
const tabCase=document.getElementsByClassName("tile");
const idSpan = document.getElementById("idSpan");

console.log(idSpan);
// fonction reset elle reinitialise les cases et le joueur en cours
const reset = ()=>{
  for (let i=0;i<9;i++)
  {
    if(tabCase[i].classList[1]=="playerX")
    {
      tabCase[i].classList.remove("playerX")
    }else if (tabCase[i].classList[1]=="playerY")
    {
      tabCase[i].classList.remove("playerY")
    }
    tabCase[i].classList.add('cache');
    
    
  }
  changeJoueur(getRandomInt(2));
}
const changeJoueur = (a) =>{
  console.log("je fais le changement de joueur");
    if (verifieSiGagne())
    {
      if (joueurEnCours==0)
    {
      console.log('joueur 0 a gagné')

    }else{
      console.log('joueur 1 a gagné')
    }
    }
    joueurEnCours=a;
    console.log(idSpan);


}
/************************************************************************** */
  /*                          FUNCTION testGagne                         */
  /************************************************************************** */
  /*  Cette fonction vérifie si il y a un gagnant                             */
  /************************************************************************** */
const testGagne = (tabMatrice,joueur)=>{
  
  let test = false;
  if (joueur == 0) {
      if (
        (tabMatrice[0][0] == "X" &&
          tabMatrice[0][1] == "X" &&
          tabMatrice[0][2] == "X") ||
        (tabMatrice[1][0] == "X" &&
          tabMatrice[1][1] == "X" &&
          tabMatrice[1][2] == "X") ||
        (tabMatrice[2][0] == "X" &&
          tabMatrice[2][1] == "X" &&
          tabMatrice[2][2] == "X") ||
        (tabMatrice[0][0] == "X" &&
          tabMatrice[1][0] == "X" &&
          tabMatrice[2][0] == "X") ||
        (tabMatrice[0][1] == "X" &&
          tabMatrice[1][1] == "X" &&
          tabMatrice[2][1] == "X") ||
        (tabMatrice[0][2] == "X" &&
          tabMatrice[1][2] == "X" &&
          tabMatrice[2][2] == "X") ||
        (tabMatrice[0][0] == "X" &&
          tabMatrice[1][1] == "X" &&
          tabMatrice[2][2] == "X") ||
        (tabMatrice[2][0] == "X" &&
          tabMatrice[1][1] == "X" &&
          tabMatrice[0][2] == "X")
      ) {
         test = true;
      } else {
         test = false;
      }
    } else {
      if (
        (tabMatrice[0][0] == "Y" &&
          tabMatrice[0][1] == "Y" &&
          tabMatrice[0][2] == "Y") ||
        (tabMatrice[1][0] == "Y" &&
          tabMatrice[1][1] == "Y" &&
          tabMatrice[1][2] == "Y") ||
        (tabMatrice[2][0] == "Y" &&
          tabMatrice[2][1] == "Y" &&
          tabMatrice[2][2] == "Y") ||
        (tabMatrice[0][0] == "Y" &&
          tabMatrice[1][0] == "Y" &&
          tabMatrice[2][0] == "Y") ||
        (tabMatrice[0][1] == "Y" &&
          tabMatrice[1][1] == "Y" &&
          tabMatrice[2][1] == "Y") ||
        (tabMatrice[0][2] == "Y" &&
          tabMatrice[1][2] == "Y" &&
          tabMatrice[2][2] == "Y") ||
        (tabMatrice[0][0] == "Y" &&
          tabMatrice[1][1] == "Y" &&
          tabMatrice[2][2] == "Y") ||
        (tabMatrice[2][0] == "Y" &&
          tabMatrice[1][1] == "Y" &&
          tabMatrice[0][2] == "Y")
      ) {
        test = true;
      } else {
        test = false;
      }
    }
    return test;
}
/************************************************************************** */
  /*                          FUNCTION recupMatrice                           */
  /************************************************************************** */
  /*  Cette fonction renvoie une matrice avec les X et les Y rempli           */
  /************************************************************************** */
  const recupMatrice=()=> {
    let tabMatrice = [
      ["", "", ""],
      ["", "", ""],
      ["", "", ""],
    ];
    let x = 0;
    let y = 0;
    
    const tabCase = Array.from(document.getElementsByClassName("tile"));
    tabCase.forEach( (item)=> {
      if (item.classList.contains("playerY")) {
        tabMatrice[y][x] = "Y";
      } else if (item.classList.contains("playerX")) {
        tabMatrice[y][x] = "X";
      }
      x++;
      if (x > 2) {
        x = 0;
        y++;
      }
    });
  
    return tabMatrice;
  }

/************************************************************************** */
  /*                          FUNCTION verifieSiGagne                         */
  /************************************************************************** */
  /*  Cette fonction vérifie si il y a un gagnant                             */
  /************************************************************************** */
  const verifieSiGagne=()=> {
    console.log('je fait verifieSiGagne')
    let gagne = false;
    let tabMatrice = recupMatrice();
    console.log(tabMatrice);
    gagne = testGagne(tabMatrice, joueurEnCours);
  
    return gagne;
  }

// fonction qui définit ce qu'il se passe si on clique sur une case
const cliqueSur = (a) => {
  // est ce que la case est cachée
  if(tabCase[a].classList[1]=="cache")
  {
    // on supprime la classe cache
    tabCase[a].classList.remove("cache");
    // si c'est plaer X qui joue
    if (joueurEnCours==0)
    {
      //on ajoute la classe playerX
      tabCase[a].classList.add('playerX');
      // on change de joueur
      changeJoueur(1);
    //sinon
    }else{
      //on ajoute la classe playerY
      tabCase[a].classList.add('playerY');
      // on change de joueur
      changeJoueur(0);
    }
  }else{
    // si la case a déjà été cliqué il ne se passe rien
    console.log("non ce n'est pas caché");
  }
  
} 
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style >
body {
    font-family: "Itim", cursive;
  font-weight: 400;
  font-style: normal;
}
h1{

  color : white;
}
h3 {
  margin: 40px 0 0;
}
ul {
  list-style-type: none;
  padding: 0;
}
li {
  display: inline-block;
  margin: 0 10px;
}
a {
  color: #42b983;
}
.background{
    background-color: #1f1f1f;
    padding :2rem;
}
.container{
  font-family: "Itim", cursive;
  font-weight: 400;
  font-style: normal;
    margin-top: 2rem;
    margin-bottom: 2rem;
   
    display: flex;
	  flex-wrap: wrap;
	  border-top: 0 !important;
    width : 35vh;
    justify-content: center;
    margin-left: auto;
    margin-right: auto;
}

.tile{
    
    width: 10vh;
    height: 10vh;
    border :1px solid white;
    color :white;
    text-align: center;
    font-size: 5rem;
    display: flex;
    justify-content: center;
    align-items: center;

}
.tile:hover{
    background-color: #a6a4a4;
}

.playerX{
   
   color : green
}

.playerY{
  
   color:red
}

.cache{
   color: #1f1f1f;
}
.controls{
    text-align: center;

}

#reset{
    background-color: red;
    padding: 1rem;
    color: white;
    border-radius: 1rem;
    border: 0px;
    margin: 3rem;
}
.display{
  font-family: "Itim", cursive;
  font-weight: 400;
  font-style: normal;
    color: white;
    font-size: 1.5rem;
    text-align: center;

}
.display-player{
    font-size: 2.5rem;

}
</style>
