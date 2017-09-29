
<!-- Template code to display the application -->
<template>
    <div class="vote">
        
        <div class="wrapper">
            <!-- Left hand column -->
            <div class="box box1">
                <div class="intro">
                    <img src="https://ronan-oleary.com/wp/wp-content/uploads/2017/09/codewars.png"/>
                    <h2 class="leadtitle">{{ leadtitle }}</h2>
                    <br>
                    <p>It is 2017 and the battle of the javascript frameworks rages in the hearts, minds and dev-environments of coders/nerds the world over.</p>
                    <p>It's hard to predict who'll emerge victorious, and with many conflicting opinions abound, it seems logical to put it to a vote.</p>
                    <p>Use the simple upvote/downvote mechanism to select your preference...</p>
                    <br>
                    <p>If in doubt, Maximilian Schwarzmüller (from Academind) has an excellent comparison video, click the button below to display.</p>
                    
                    <!-- Simple toggle effect -->
                    <button class="btn" v-on:click="display = !display">
                        <span v-if="display">Hide Video</span>
                        <span v-else>Show Video</span>
                    </button>
                    <br><br>
                    <iframe v-if="display" width="80%" height="450" src="https://www.youtube.com/embed/KMX1mFEmM3E" frameborder="0" allowfullscreen></iframe>
                </div>
            </div>
            <div class="box box2">
                <!-- Display current leader -->
                <div> 
                    <h2>Current leader is <span class="currentLeader">{{ leader.name }}</span></h2>
                    <img class="logo" v-bind:src="leader.framework_img"/> 
                    <img class="logo" v-bind:src="leader.img"/>
                    <br>
                </div>
            </div>
            <div class="box box3">
                <p>Spun up by <a href="https://ronan-oleary.com" target="_blank">Danger Ro</a></p>
            </div>
            <div class="box box4">
                
                <div class="nested">
                    <!-- Actual vote -->
                    <ul class="list-group">  
                        <h2>HAVE YOUR SAY!</h2>   
                        <small>(Psssst....in a real-world app, we'd limit the number of up/down votes so people couldn't cheat)</small>   
                        <br>
                        <li class="list-group-item" v-for="framework in frameworks" v-bind:class="{ currentRuler:framework.isCurrentLeader }">

                            <img class="char-image" v-bind:src="framework.framework_img" />
                            
                            <div class="main-content">
                                <p><strong>Name:</strong> {{ framework.name }}</p>
                                <p><strong>Created By: </strong>{{ framework.creators }}</p>	
                                <p><strong>Lang: </strong>{{ framework.uses }}</p>	
                                <p><strong>Difficulty: </strong>{{ framework.difficulty }}</p>		
                                <p><strong>Released: </strong>{{ framework.year }}</p>		
                                <p><strong>Link: <a v-bind:href="framework.link" target="_blank">Docs</a></strong></p>
                           
                                <h3><strong>Votes: {{ framework.votes }}</strong></h3>
                           
                                <br>
                           
                                <button class="btn" @click="framework.votes++">Up Vote</button>
                                <button class="btn" @click="framework.votes--">Down Vote</button>
                            </div>
                        </li>
                    </ul>
                </div>
            </div>
        </div>
	</div>
    
</template>
<!-- End template output, start script -->
<script>
export default {
  name: 'vote',
  data () {
    return {
        display: false,
        leadtitle: "Who will win the battle of the JS Frameworks?", 
        // in a real-world situation, we would pull json from an external resource or endpoint
        frameworks: [
            {
                name: 'Vue JS',
                votes: 5,
                creators: 'Evan Yu',
                uses: 'javascript',
                year: '2013',
                difficulty: 'easy', 
                framework_img: 'https://ronan-oleary.com/wp/wp-content/uploads/2017/09/vue.png',
                img: 'https://ronan-oleary.com/wp/wp-content/uploads/2017/09/evanyou.jpeg',
                link: 'https://vuejs.org/',
                isCurrentLeader: false
            },
            {
                name: 'React',
                votes: 7,
                creators: 'Facebook',
                uses: 'JSX',
                year: '2013',
                difficulty: 'medium-hard', 
                framework_img: 'https://ronan-oleary.com/wp/wp-content/uploads/2017/09/reactlogo.png',
                img: 'https://ronan-oleary.com/wp/wp-content/uploads/2017/09/fb.png',
                link: 'https://facebook.github.io/react',
                isCurrentLeader: false
            },
            {
                name: 'Angular JS',
                votes: 3,
                creators: 'Google',
                uses: 'Typescript',
                year: '2016',
                difficulty: 'medium', 
                framework_img: 'https://ronan-oleary.com/wp/wp-content/uploads/2017/09/ang4.png',
                img: 'https://ronan-oleary.com/wp/wp-content/uploads/2017/09/google.png',
                link: 'https://angular.io/',
                isCurrentLeader: false
            }
        ]}
    },
    methods: {
        // probably going to lose this, a simple reset, doesn't change the order, just kills the votes 
        reset() {
            this.frameworks = this.frameworks.map(function(framework) {
                framework.votes = 0;
                return framework;
            })
        }
    },
    computed: {
        leader() {
            var currentLeader = 	this.frameworks.sort(function(a, b) {
                return b.votes - a.votes;
            });
            
            if(currentLeader[0]){
                currentLeader[0].isCurrentLeader = true;
            }
            currentLeader[0].isCurrentLeader = false;
            return currentLeader[0];
            
        }
    }
}


</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>


.wrapper{
    display: grid; 
    grid-template-columns: repeat(1fr 2fr);
    grid-auto-rows: minmax(50px, auto); 
    grid-gap: 1em; 
    justify-items:stretch;
    align-items: stretch;  
}

.wrapper > div{
    background: #eee; 
    padding: 1em; 
}

.wrapper > div:nth-child(odd){
    background: #ddd;
    
}

.box1{
    grid-column: 1/2;
    grid-row: 1/3;
    
}

.leadtitle{
    font-size: 55px;    
}

.intro{
   align-self: center;
   padding-top: 10%;  
}

.intro p{
    font-size: 20px; 
}

.box2{
    /* align-self: end;  */
    grid-column: 2/4;
    grid-row: 1;
    background: #000; 
}

.box3{
    /* justify-self: end;  */
    grid-column: 1/4;
    grid-row: 3/4;

}

.box4{
    /* align-self: end;  */
    grid-column: 2/4;
    grid-row: 2;
}


.nested{
    display: grid; 
    grid-template-columns:repeat(1fr, 3fr);
    grid-auto-rows: minmax(70px);
    grid-gap: 1em; 
}

.nested > div {
    border: 1px solid darkred;
    padding: 1em .5em;
}

.logo, .char-image{
    width: 150px;
    height: 150px; 
}

@media screen and (max-width: 650px){

   .list-group-item{
        display: grid;
        margin: 0 0 10px 0;
    }
   
   .box1{
        grid-column: 1/4;
        grid-row: 1;
        align-items: center; 
        background-color: pink; 
    }

    .leadtitle{
        font-size: 35px;    
    }

    .intro{
        align-self: center;
        padding-top: 0%;  
        padding-bottom: 5%;
    }

    .box2{
        grid-column: 1/4;
        grid-row: 2;
    }
    .box3{
        grid-column: 1/4;
        grid-row: 4
    }

    .box4{
        grid-column: 1/4;
        grid-row: 3;
        border: 1px  green solid; 
    }

    .char-image{
        width: 70px; 
        height: 75px; 
    }
}


.fade-enter-active, .fade-leave-active {
  transition: opacity .5s
}
.fade-enter, .fade-leave-to /* .fade-leave-active in <2.1.8 */ {
  opacity: 0
}


h1, h2{
  font-weight: normal;
   color: #000;  
}

h3, p{
    font-weight: normal;
    color: #333;
}

.currentLeader{
    color: red;
    font-weight: bold;  
}


.list-group{
    display: grid; 
}
.list-group-item{
    display: inline-flex;
    margin: 0 0 10px 0;
    width: 100%;
}

.main-content{
    text-align: left;
    padding: 2px 5px;
}

a {
  color: #42b983;
}


</style>


  