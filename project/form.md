## 1. checkbox
```js
/*
checkbox复选框实现全选
 * */

//最好不要用attr方法增加属性，否则会出现第三次点击不生效的情况，用prop方法较好
$('input[name="selectall"]').click(function(){  
        //alert(this.checked);  
        if($(this).is(':checked')){  
            $('input[name="stuCheckBox"]').each(function(){  
                //此处如果用attr，会出现第三次失效的情况  
                $(this).prop("checked",true);  
            });  
    }else{  
        $('input[name="stuCheckBox"]').each(function(){  
                $(this).removeAttr("checked",false);  
            });  
            //$(this).removeAttr("checked");  
    }         
});  
```