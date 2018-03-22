# es6

    util1.js util2.js index.js

    util1.js
    
    export default{
    
        a:100
      
    }
    
    util2.js

    export fn1()=>{

        console.log('我是fn1');

    }
    
    export fn2()=>{
    
        console.log('我是fn2')
      
    }
    
    index.js

    import util1 from ./util1.js

    import {fn1,fn2} from ./util2.js

    
  
  
