---
layout: page
title: Wiki
---
<div class="wiki">
    <a href="http://zh.wikipedia.org/zh/JavaScript"><h2>Javascript</h2></a>
    
    <ul class="hide">
        <li><a href="http://jqfundamentals.com/book/index.html">
    	jQuery Fundamentals</a> -jQuery 入门教程。</li>
    </ul>
    
    <a href="http://en.wikipedia.org/wiki/Robert_Lucas,_Jr."><h2>J.R.Lucas</h2></a>
</div>
<script type="text/javascript">
    $(document).ready(function(){
        $('#content a').each(function(index,element){
            var href = $(this).attr('href');
            if(href.indexOf('#') == 0){
            }else if ( href.indexOf('/') == 0 || href.toLowerCase().indexOf('beiyuu.com')>-1 ){
                $(this).attr('target','_blank');
            }else{
                $(this).attr('target','_blank');
                $(this).addClass('external');
            }
        });
        $('body').delegate('h2','click',function(e){
            e.preventDefault();
            $(this).next('ul').toggle();
        });
    });
</script>  