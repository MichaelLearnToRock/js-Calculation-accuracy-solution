# js-
js防止精度丢失（加减乘除）
在原生Number.prototype上重新扩展加减乘除的方法
  
    
      //加法   
    Number.prototype.add = function(arg){   
        var r1,r2,m;   
        try{r1=this.toString().split(".")[1].length}catch(e){r1=0}   
        try{r2=arg.toString().split(".")[1].length}catch(e){r2=0}   
        m=Math.pow(10,Math.max(r1,r2))   
        return (this.mul(m) + arg.mul(m)) / m;   
    }  
    //减法   
    Number.prototype.sub = function (arg){   
        return this.add(-arg);   
    }   

    //乘法   
    Number.prototype.mul = function (arg)   
    {   
        var m=0,s1=this.toString(),s2=arg.toString();   
        try{m+=s1.split(".")[1].length}catch(e){}   
        try{m+=s2.split(".")[1].length}catch(e){}   
        return Number(s1.replace(".",""))*Number(s2.replace(".",""))/Math.pow(10,m)   
    }   

    //除法   
    Number.prototype.div = function (arg){   
        var t1=0,t2=0,r1,r2;   
        try{t1=this.toString().split(".")[1].length}catch(e){}   
        try{t2=arg.toString().split(".")[1].length}catch(e){}   
        with(Math){   
            r1=Number(this.toString().replace(".",""))   
            r2=Number(arg.toString().replace(".",""))   
            return (r1/r2)*pow(10,t2-t1);   
        }   
    }
