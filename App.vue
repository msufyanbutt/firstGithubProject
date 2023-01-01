<template>
  <div id="app">
    <div class="bg-black w-full h-screen ">
      <div class=" w-64 h-80 m-auto ">
          <div class="flex flex-col pt-20 ">
           <div><p class="text-gray-400 text-sm text-center pb-4">Password Generator</p></div>
            
            <div class="w-full h-12 bg-gray-700 opacity-50 text-white">
           <div class="flex flex-row justify-between px-4 py-2 ">
            

            <p v-if="newPassword" class="hover:text-white">{{newPassword}}</p>
            <p id="butt" class="text-gray-300 " v-else-if="selectedCapitalBox" >{{selectedCapitalBox}}</p>
            <p v-else-if="selectedSmallBox">{{selectedSmallBox}}</p>
            <p v-else-if="selectedNumberBox">{{selectedNumberBox}}</p>
            <p v-else-if="selectedSymbolBox">{{selectedSymbolBox}}</p>
            <p v-else>{{defaultpasswords}}</p>
            <span class=""></span>
            <span @click.prevent="copyclipBoard()"  class="mdi mdi-content-copy text-green-300 cursor-pointer" ></span>

           </div>
          </div>


          
      

          </div>

          
      

          <div class="flex flex-col w-full h-96  my-4 bg-gray-700 opacity-50 px-2 ">
            <div class="flex flex-row justify-between px-2 py-2">
              <p class="text-white">Character Length</p>
              <span class="text-green-400">{{CharacterLenght}}</span>
            </div>
            <div class="flex flex-row justify-evenly py-2  ">
              <span @click="MinuscharacterLength()" class="mdi mdi-minus text-white font-bold cursor-pointer  hover:bg-gray-100 rounded-sm hover:text-black pt-1"></span>
              <input type="range" class="w-44 h-1 cursor-pointer mt-3.5" >
              <span @click ="AddcharacterLength()" class="mdi mdi-plus pt-1 font-bold cursor-pointer text-white hover:bg-gray-100 rounded-sm hover:text-black"></span>
            </div>
            <div class="flex flex-row hover:bg-gray-400 " >
              <input type="checkbox"  class="mx-2 my-2 " v-model="selectedCapitalBox">
              
              <p class="text-white ">Include Uppercase Letters</p>

              
            </div>

            <div class="flex flex-row  hover:bg-gray-400" >
              <input type="checkbox"  v-model="selectedSmallBox" class="mx-2 my-2 ">
              
              <p class="text-white ">Include LowerCase Letters</p>
            </div>
            <div class="flex flex-row hover:bg-gray-400" >
              <input type="checkbox"  v-model="selectedNumberBox" class="mx-2 my-2 ">
              
              <p class="text-white ">Include Numbers</p>
            </div>
            <div class="flex flex-row hover:bg-gray-400" >
              <input type="checkbox"  value="$1" v-model="selectedSymbolBox" class="mx-2 my-2 ">
              
              <p class="text-white " >Include Symbols</p>
            </div>


            <div class="flex flex-row w-56 h-8 bg-black text-white px-2 py-1 justify-between  my-2 mx-2 cursor-pointer">
              <p class="uppercase text-xm text-gray-400 hover:text-green-500">Strength</p>
              <p v-if="this.CharacterLenght==0" class=" mdi mdi-wifi hover:text-gray-500"></p>
              <p v-else-if="this.CharacterLenght==1" class="text-green-700 mdi mdi-wifi hover:text-gray-500"></p>  
              <p v-else-if="this.CharacterLenght==2" class="text-green-700 mdi mdi-wifi hover:text-gray-500"></p>
              <p v-else-if="this.CharacterLenght==3" class="text-green-700 mdi mdi-wifi hover:text-gray-500"></p>
              <p v-else-if="this.CharacterLenght==4" class="text-green-700 mdi mdi-wifi hover:text-gray-500"></p>
              <p v-else-if="this.CharacterLenght==5" class="text-green-700 mdi mdi-wifi hover:text-gray-500"></p>
              <p v-else-if="this.CharacterLenght==6" class="text-blue-600 mdi mdi-wifi hover:text-gray-500"></p>
              
              <p v-else-if="this.CharacterLenght==7" class="text-blue-300 mdi mdi-wifi hover:text-gray-500"></p>
              
              <p v-else-if="this.CharacterLenght==8" class="text-blue-600 mdi mdi-wifi hover:text-gray-500"></p>
              
              <p v-else-if="this.CharacterLenght==9" class="text-red-600 mdi mdi-wifi hover:text-gray-500"></p>
              <p v-else-if="this.CharacterLenght==10" class="text-red-600 mdi mdi-wifi hover:text-gray-500"></p>
              <p v-else class="mdi mdi-wifi text-green-500 hover:text-gray-500"></p>
            </div>

            <div 
            @click = " generatePassword()  "
            
            class="flex flex-row w-56 h-8 bg-green-300 text-white px-2 py-2 justify-between  my-2 mx-2  hover:bg-gray-50 cursor-pointer">
              <div class="flex flex-row " >
                <p class="text-xs text-black ml-16 ">GENERATE</p>
                
              </div>

            </div>

            <div 

                @click="resetFun()"

            class="flex flex-row w-56 h-8 bg-gray-300 text-white px-2 py-2 justify-between  my-4 mx-2  hover:bg-red-600">
              <div class="flex flex-row " >
                <p class="text-xs text-black ml-20 font-bold cursor-pointer">RESET</p>
                
              </div>

            </div>

            
          </div>
        </div>

      
    </div>    

  </div>
</template>

<script>
  export default{
      name:"app",
      data() {
        return {
          
          password1:"0000", 
          upper:"but",
          capital:"fill",
          small:"fill",
          number:0,
          symbol:"",
          message:"",
          selectedCapitalBox:"",
          selectedSmallBox:"",
          selectedNumberBox:"",
          selectedSymbolBox:"",
          defaultpasswords:"",
          CharacterLenght:0,
          newPassword : "",
          CharacterLengthLOOp:[1,2,3,4,5,6,7,8,9,10],
          EasyStrength:"Easy",
          mediumStrength:"Medium",
          HardStrength:"Hard",

          // selectedBoxes:{
          //     capitalLetter:"",
          //     smallLetter:"",
          //     numbers:'',
          //     symbols:'',
          // },
          }
          
        },

        methods:{
          generatePassword  () {
            if(this.CharacterLenght==0 && this.selectedCapitalBox){
              this.newPassword = this.selectedCapitalBox;
            }
            if(this.CharacterLenght == 1 && this.selectedCapitalBox){
              this.newPassword = "A";
            }
            if(this.CharacterLenght == 2 && this.selectedCapitalBox){
              this.newPassword = "GH";
            }
            if(this.CharacterLenght == 3 && this.selectedCapitalBox){
              this.newPassword = "JKC";
            }
            
            if(this.CharacterLenght == 4 && this.selectedCapitalBox){
              this.newPassword = "UIOW";
            }
            if(this.CharacterLenght == 5 && this.selectedCapitalBox){
              this.newPassword = "YUEHI";
            }
            
            if(this.CharacterLenght == 6 && this.selectedCapitalBox){
              this.newPassword = "TYUEBI";
            }
            
            if(this.CharacterLenght == 7 && this.selectedCapitalBox){
              this.newPassword = "OPUYREQ";
            }
            
            if(this.CharacterLenght == 8 && this.selectedCapitalBox){
              this.newPassword = "ZXCVBATU";
            }
            
            if(this.CharacterLenght == 9 && this.selectedCapitalBox){
              this.newPassword = "RWEQHVSIP";
            }
            
            if(this.CharacterLenght == 10 && this.selectedCapitalBox){
              this.newPassword = "QWUYEIOUBV";
            }
            if(this.CharacterLenght == 0 && this.selectedSmallBox){
              this.newPassword = this.selectedSmallBox;
            }
            if(this.CharacterLenght == 1 && this.selectedSmallBox){
              this.newPassword = "m";
            }
            if(this.CharacterLenght == 2 && this.selectedSmallBox){
              this.newPassword = "ui";
            }
            if(this.CharacterLenght == 3 && this.selectedSmallBox){
              this.newPassword = "fri";
            }
            
            if(this.CharacterLenght == 4 && this.selectedSmallBox){
              this.newPassword = "rtwe";
            }
            if(this.CharacterLenght == 5 && this.selectedSmallBox){
              this.newPassword = "lkrst";
            }
            
            if(this.CharacterLenght == 6 && this.selectedSmallBox){
              this.newPassword = "pouwrb";
            }
            
            if(this.CharacterLenght == 7 && this.selectedSmallBox){
              this.newPassword = "qwtdvsd";
            }
            
            if(this.CharacterLenght == 8 && this.selectedSmallBox){
              this.newPassword = "reyquvcx";
            }
            
            if(this.CharacterLenght == 9 && this.selectedSmallBox){
              this.newPassword = "mnopfgetu";
            }
            
            if(this.CharacterLenght == 10 && this.selectedSmallBox){
              this.newPassword = "asdfghjklo";
            }
            if(this.CharacterLenght == 0 && this.selectedNumberBox){
              this.newPassword = this.selectedNumberBox;
            }
            if(this.CharacterLenght == 1 && this.selectedNumberBox){
              this.newPassword = "5";
            }
            if(this.CharacterLenght == 2 && this.selectedNumberBox){
              this.newPassword = "32";
            }
            if(this.CharacterLenght == 3 && this.selectedNumberBox){
              this.newPassword = "892";
            }
            
            if(this.CharacterLenght == 4 && this.selectedNumberBox){
              this.newPassword = "8899";
            }
            if(this.CharacterLenght == 5 && this.selectedNumberBox){
              this.newPassword = "09235";
            }
            
            if(this.CharacterLenght == 6 && this.selectedNumberBox){
              this.newPassword = "827534";
            }
            
            if(this.CharacterLenght == 7 && this.selectedNumberBox){
              this.newPassword = "2436576";
            }
            
            if(this.CharacterLenght == 8 && this.selectedNumberBox){
              this.newPassword = "24563874";
            }
            
            if(this.CharacterLenght == 9 && this.selectedNumberBox){
              this.newPassword = "243849709";
            }
            
            if(this.CharacterLenght == 10 && this.selectedNumberBox){
              this.newPassword = "5438394546";
            }
            
            if(this.CharacterLenght == 0 && this.selectedSymbolBox){
              this.newPassword = this.selectedSymbolBox;
            }
            if(this.CharacterLenght == 1 && this.selectedSymbolBox){
              this.newPassword = "@";
            }
            if(this.CharacterLenght == 2 && this.selectedSymbolBox){
              this.newPassword = "!#";
            }
            if(this.CharacterLenght == 3 && this.selectedSymbolBox){
              this.newPassword = "^&%";
            }
            
            if(this.CharacterLenght == 4 && this.selectedSymbolBox){
              this.newPassword = "!@!@";
            }
            if(this.CharacterLenght == 5 && this.selectedSymbolBox){
              this.newPassword = "&&$$#";
            }
            
            if(this.CharacterLenght == 6 && this.selectedSymbolBox){
              this.newPassword = "&$#@!!";
            }
            
            if(this.CharacterLenght == 7 && this.selectedSymbolBox){
              this.newPassword = "#$%^*-*";
            }
            
            if(this.CharacterLenght == 8 && this.selectedSymbolBox){
              this.newPassword = "^%$#@!$%";
            }
            
            if(this.CharacterLenght == 9 && this.selectedSymbolBox){
              this.newPassword = "#@$%^&()+";
            }
            
            if(this.CharacterLenght == 10 && this.selectedSymbolBox){
              this.newPassword = "!@#$%^&*$$";
            }

            if(this.selectedCapitalBox){
              
              this.selectedCapitalBox = "GHTYEUWM";
            }
            if(this.selectedSmallBox){
              this.selectedSmallBox = "sufibutt";
            }
            if(this.selectedNumberBox){
              this.selectedNumberBox = 12345678;
            }
            if(this.selectedSymbolBox){
              this.selectedSymbolBox = "!@#$%^&*";
            }
            if(this.selectedCapitalBox && this.selectedSmallBox){
              this.newPassword = "DEFghiYb ";
            }
            if(this.selectedCapitalBox && this.selectedSmallBox && this.selectedNumberBox){
              this.newPassword = "NMT678po";
            }
            if(this.selectedCapitalBox && this.selectedSmallBox && this.selectedNumberBox && this.selectedSymbolBox){
              this.newPassword = "gy$%SF98";
            }
            if(this.selectedSmallBox && this.selectedNumberBox && this.selectedSymbolBox){
              this.newPassword="@ry76@#9"
            }
            
            if(this.CharacterLenght==0 && this.selectedSmallBox && this.selectedNumberBox){
              this.newPassword="33asu9po"
            }
            if(this.CharacterLenght==1 && this.selectedSmallBox && this.selectedNumberBox){
              this.newPassword="8"
            }
            if(this.CharacterLenght==2 && this.selectedSmallBox && this.selectedNumberBox){
              this.newPassword="a0"
            }
            if(this.CharacterLenght==3 && this.selectedSmallBox && this.selectedNumberBox){
              this.newPassword="ad5"
            }
            if(this.CharacterLenght==4 && this.selectedSmallBox && this.selectedNumberBox){
              this.newPassword="gh76"
            }
            if(this.CharacterLenght==5 && this.selectedSmallBox && this.selectedNumberBox){
              this.newPassword="875ty"
            }
            if(this.CharacterLenght==6 && this.selectedSmallBox && this.selectedNumberBox){
              this.newPassword="ret999"
            }
            if(this.CharacterLenght==7 && this.selectedSmallBox && this.selectedNumberBox){
              this.newPassword="david88"
            }
            if(this.CharacterLenght==8 && this.selectedSmallBox && this.selectedNumberBox){
              this.newPassword="sufi3339"
            }
            if(this.CharacterLenght==9 && this.selectedSmallBox && this.selectedNumberBox){
              this.newPassword="sufyan132"
            }
            if(this.CharacterLenght==10 && this.selectedSmallBox && this.selectedNumberBox){
              this.newPassword="sufyanbutt"
            }

            if(this.CharacterLenght==0 && this.selectedCapitalBox && this.selectedNumberBox){
              this.newPassword="DHQ994"
            }
            if(this.CharacterLenght==1 && this.selectedCapitalBox && this.selectedNumberBox){
              this.newPassword="2"
            }
            if(this.CharacterLenght==2 && this.selectedCapitalBox && this.selectedNumberBox){
              this.newPassword="S5"
            }
            if(this.CharacterLenght==3 && this.selectedCapitalBox && this.selectedNumberBox){
              this.newPassword="GH4"
            }
            if(this.CharacterLenght==4 && this.selectedCapitalBox && this.selectedNumberBox){
              this.newPassword="76JK"
            }
            if(this.CharacterLenght==5 && this.selectedCapitalBox && this.selectedNumberBox){
              this.newPassword="AK479"
            }
            if(this.CharacterLenght==6 && this.selectedCapitalBox && this.selectedNumberBox){
              this.newPassword="TUTO33"
            }
            if(this.CharacterLenght==7 && this.selectedCapitalBox && this.selectedNumberBox){
              this.newPassword="RARE555"
            }
            if(this.CharacterLenght==8 && this.selectedCapitalBox && this.selectedNumberBox){
              this.newPassword="WEBDEVE77"
            }
            if(this.CharacterLenght==9 && this.selectedCapitalBox && this.selectedNumberBox){
              this.newPassword="PUNJABU56"
            }
            if(this.CharacterLenght==10 && this.selectedCapitalBox && this.selectedNumberBox){
              this.newPassword="GIFTSUNAI3"
            }



            if(this.CharacterLenght==0 && this.selectedCapitalBox && this.selectedSymbolBox){
              this.newPassword="WQRT@#U)"
             }
             if(this.CharacterLenght==1 && this.selectedCapitalBox && this.selectedSymbolBox){
              this.newPassword="@"
             }
             if(this.CharacterLenght==2 && this.selectedCapitalBox && this.selectedSymbolBox){
              this.newPassword="!I"
             }
             if(this.CharacterLenght==3 && this.selectedCapitalBox && this.selectedSymbolBox){
              this.newPassword="#S#"
             }
             
             if(this.CharacterLenght==4 && this.selectedCapitalBox && this.selectedSymbolBox){
              this.newPassword="#^HU"
             }
             
             if(this.CharacterLenght==5 && this.selectedCapitalBox && this.selectedSymbolBox){
              this.newPassword="!@#JK"
             }
             
             if(this.CharacterLenght==6 && this.selectedCapitalBox && this.selectedSymbolBox){
              this.newPassword="GTU##^"
             }
             
             if(this.CharacterLenght==7 && this.selectedCapitalBox && this.selectedSymbolBox){
              this.newPassword="GOP##^"
             }
             
             if(this.CharacterLenght==8 && this.selectedCapitalBox && this.selectedSymbolBox){
              this.newPassword="%%USE%%!"
             }
             
             if(this.CharacterLenght==9 && this.selectedCapitalBox && this.selectedSymbolBox){
              this.newPassword="$LKJDUEI$"
             }
             
             if(this.CharacterLenght==10 && this.selectedCapitalBox && this.selectedSymbolBox){
              this.newPassword="$#%@HAAJI)"
             }


             if(this.CharacterLenght==0 && this.selectedSmallBox && this.selectedSymbolBox){
              this.newPassword="ghrt$%bg"
             }
             if(this.CharacterLenght==1 && this.selectedSmallBox && this.selectedSymbolBox){
              this.newPassword="e"
             }
             if(this.CharacterLenght==2 && this.selectedSmallBox && this.selectedSymbolBox){
              this.newPassword="r$"
             }
             if(this.CharacterLenght==3 && this.selectedSmallBox && this.selectedSymbolBox){
              this.newPassword="we!"
             }
             if(this.CharacterLenght==4 && this.selectedSmallBox && this.selectedSymbolBox){
              this.newPassword="ret*"
             }
             if(this.CharacterLenght==5 && this.selectedSmallBox && this.selectedSymbolBox){
              this.newPassword="$gth%"
             }
             
             if(this.CharacterLenght==6 && this.selectedSmallBox && this.selectedSymbolBox){
              this.newPassword="iou&^%"
             }
             
             if(this.CharacterLenght==7 && this.selectedSmallBox && this.selectedSymbolBox){
              this.newPassword="zxc*&({"
             }
             
             if(this.CharacterLenght==8 && this.selectedSmallBox && this.selectedSymbolBox){
              this.newPassword="!@#$turg"
             }
             
             if(this.CharacterLenght==9 && this.selectedSmallBox && this.selectedSymbolBox){
              this.newPassword="$uyto^%&*"
             }
             
             if(this.CharacterLenght==10 && this.selectedSmallBox && this.selectedSymbolBox){
              this.newPassword="$({tyru)}$"
             }


             if(this.CharacterLenght==0 && this.selectedNumberBox && this.selectedSymbolBox){
              this.newPassword="654*&^@#"
             }
             if(this.CharacterLenght==1 && this.selectedNumberBox && this.selectedSymbolBox){
              this.newPassword="%"
             }
             if(this.CharacterLenght==2 && this.selectedNumberBox && this.selectedSymbolBox){
              this.newPassword="5$"
             }
             if(this.CharacterLenght==3 && this.selectedNumberBox && this.selectedSymbolBox){
              this.newPassword="!7%"
             }
             
             if(this.CharacterLenght==4 && this.selectedNumberBox && this.selectedSymbolBox){
              this.newPassword="98%$"
             }
             
             if(this.CharacterLenght==5 && this.selectedNumberBox && this.selectedSymbolBox){
              this.newPassword="@34%#"
             }
             
             if(this.CharacterLenght==6 && this.selectedNumberBox && this.selectedSymbolBox){
              this.newPassword="^&098@"
             }
             
             if(this.CharacterLenght==7 && this.selectedNumberBox && this.selectedSymbolBox){
              this.newPassword="($%799)"
             }
             
             if(this.CharacterLenght==8 && this.selectedNumberBox && this.selectedSymbolBox){
              this.newPassword="#{8756}$"
             }
             
             if(this.CharacterLenght==9 && this.selectedNumberBox && this.selectedSymbolBox){
              this.newPassword="^76532(*)"
             }
             
             if(this.CharacterLenght==10 && this.selectedNumberBox && this.selectedSymbolBox){
              this.newPassword="@098@63*&^"
             }



            if(this.CharacterLenght == 0 && this.selectedCapitalBox && this.selectedSmallBox){
              this.newPassword = "SDKJuioP";
            }
            if(this.CharacterLenght==1 && this.selectedCapitalBox && this.selectedSmallBox){
              this.newPassword= "x";
            }
            if(this.CharacterLenght==2 && this.selectedCapitalBox && this.selectedSmallBox){
              this.newPassword = "hG";
            }
            if(this.CharacterLenght == 3 && this.selectedCapitalBox && this.selectedSmallBox){
              this.newPassword = "Suf";
            }
            if(this.CharacterLenght==4 && this.selectedCapitalBox && this.selectedSmallBox){
              this.newPassword="Fyti";

            }
            if(this.CharacterLenght==5 && this.selectedCapitalBox && this.selectedSmallBox){
              this.newPassword = "RusnS";
            }
            if(this.CharacterLenght==6 && this.selectedCapitalBox && this.selectedSmallBox){
              this.newPassword = "QweDhj";

            }
            if(this.CharacterLenght==7 && this.selectedCapitalBox && this.selectedSmallBox){
              this.newPassword = "TyeRRop";
            }
            if(this.CharacterLenght==8 && this.selectedCapitalBox && this.selectedSmallBox){
              this.newPassword="QRbbUUpo";
            }
            if(this.CharacterLenght==9 && this.selectedCapitalBox && this.selectedSmallBox){
              this.newPassword="ZXCnjopYt"
            }
            if(this.CharacterLenght==10 && this.selectedCapitalBox && this.selectedSmallBox){
              this.newPassword="DFcyioePPy"
            }


            if(this.CharacterLenght==0 && this.selectedCapitalBox && this.selectedSmallBox && this.selectedNumberBox){
              this.newPassword = "98GHutio";
            }
            
            if(this.CharacterLenght==1 && this.selectedCapitalBox && this.selectedSmallBox && this.selectedNumberBox){
              this.newPassword="q";
            }
            
            if(this.CharacterLenght==2 && this.selectedCapitalBox && this.selectedSmallBox && this.selectedNumberBox){
              this.newPassword="2o"
            }
            
            if(this.CharacterLenght==3 && this.selectedCapitalBox && this.selectedSmallBox && this.selectedNumberBox){
              this.newPassword="0oG"
            }
            
            if(this.CharacterLenght==4 && this.selectedCapitalBox && this.selectedSmallBox && this.selectedNumberBox){
              this.newPassword="Aq0i"
            }
            
            if(this.CharacterLenght==5 && this.selectedCapitalBox && this.selectedSmallBox && this.selectedNumberBox){
              this.newPassword="98Li0"
            }
            
            if(this.CharacterLenght==6 && this.selectedCapitalBox && this.selectedSmallBox && this.selectedNumberBox){
              this.newPassword="dfgt8B"
            }
            
            if(this.CharacterLenght==7 && this.selectedCapitalBox && this.selectedSmallBox && this.selectedNumberBox){
              this.newPassword="GTR90xx"
            }
            
            if(this.CharacterLenght==8 && this.selectedCapitalBox && this.selectedSmallBox && this.selectedNumberBox){
              this.newPassword="5467mMhy"
            }
            
            if(this.CharacterLenght==9 && this.selectedCapitalBox && this.selectedSmallBox && this.selectedNumberBox){
              this.newPassword="HHUI654po"
            }
            
            if(this.CharacterLenght==10 && this.selectedCapitalBox && this.selectedSmallBox && this.selectedNumberBox){
              this.newPassword="7876Iioo00"
            }

            if(this.CharacterLenght==0 && this.selectedCapitalBox && this.selectedNumberBox && this.selectedSmallBox && this.selectedSymbolBox){
              this.newPassword="@fgrRp0o"
            }
            if(this.CharacterLenght==1 && this.selectedCapitalBox && this.selectedSmallBox && this.selectedNumberBox && this.selectedSymbolBox){
              this.newPassword="$"
            }
            if(this.CharacterLenght==2 && this.selectedCapitalBox && this.selectedSmallBox && this.selectedNumberBox && this.selectedSymbolBox){
              this.newPassword="Gt"
            }
            
            if(this.CharacterLenght==3 && this.selectedCapitalBox && this.selectedSmallBox && this.selectedNumberBox && this.selectedSymbolBox){
              this.newPassword="*Up"
            }
            
            if(this.CharacterLenght==4 && this.selectedCapitalBox && this.selectedSmallBox && this.selectedNumberBox && this.selectedSymbolBox){
              this.newPassword="A#b9"
            }
            
            if(this.CharacterLenght==5 && this.selectedCapitalBox && this.selectedSmallBox && this.selectedNumberBox && this.selectedSymbolBox){
              this.newPassword="Hu^#0"
            }
            
            if(this.CharacterLenght==6 && this.selectedCapitalBox && this.selectedSmallBox && this.selectedNumberBox && this.selectedSymbolBox){
              this.newPassword="@@#Gi0"
            }
            
            if(this.CharacterLenght==7 && this.selectedCapitalBox && this.selectedSmallBox && this.selectedNumberBox && this.selectedSymbolBox){
              this.newPassword="%ytJK98"
            }
            
            if(this.CharacterLenght==8 && this.selectedCapitalBox && this.selectedSmallBox && this.selectedNumberBox && this.selectedSymbolBox){
              this.newPassword="we0reLO#"
            }
            
            if(this.CharacterLenght==9 && this.selectedCapitalBox && this.selectedSmallBox && this.selectedNumberBox && this.selectedSymbolBox){
              this.newPassword="%4%@$4sdI"
            }
            
            if(this.CharacterLenght==10 && this.selectedCapitalBox && this.selectedSmallBox && this.selectedNumberBox && this.selectedSymbolBox){
              this.newPassword="QWE876*^#p"
            }


            if( this.CharacterLenght==0 && this.selectedCapitalBox && this.selectedNumberBox && this.selectedSymbolBox){
              this.newPassword="@QTR898$"
            }
           
            

            
            
            if(this.CharacterLenght <0){
              this.newPassword="Please! Select positive";
            }
            if(this.CharacterLenght >10){
              alert("sorry! You can Select only 10 characters Length");
              this.newPassword = "oops! only select 10 Length";
            }
            
            else{
              this.defaultpasswords = "abju65#$";
            }
            
          
          },

                        
            resetFun(){
              alert("Are you sure you want to reset password ?");
              this.selectedCapitalBox = "";
              this.selectedSmallBox = "";
              this.selectedNumberBox = "";
              this.selectedSymbolBox = "";
              this.defaultpasswords = "";
              this.newPassword = "";
              this.CharacterLenght = 0; 
            },
            copyclipBoard(){

              const el =document.createElement('textarea')

              el.setAttribute('readonly' ,'')
              el.style.position ='absolute'

              el.style.left ='-9999px'
              
              el.value =` ${this.newPassword || this.defaultpasswords }`

              document.body.appendChild(el);
              el.select();
              document.execCommand('copy');
              alert("copied the Password on ClipBoard")
              document.body.removeChild();


              // alert("Copy");
              // var vm ;
              // var copyText = vm.$refs.butt;
              // copyText.select();
              // document.execCommand("copy");

              // alert("Cpoy : " + copyText.value);
            },
            AddcharacterLength(){
                this.CharacterLenght++;
            },
            MinuscharacterLength(){
                this.CharacterLenght--;
            },

        
      }
  }
</script>



