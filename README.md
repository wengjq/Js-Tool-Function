# Js-Tool-Function
一些 js 工具函数及题目

## 去除字符串两端空格
    
    function trim(string) {
      if (!string) {
        return string;
      }
      if (string) {
        return string.trim();
      }
      return (string + "").replace(/^[\s\uFEFF\xA0]+|[\s\uFEFF\xA0]+$/g, "");
    }
    
## 原生 js 实现 jquery 的 slideUp 和 slideDown 方法

	function morph(element, options, animationTime, callback) { 
	    var ComputedElementStyle = window.getComputedStyle(element,null);
	    var AttrElementStyle = element.style;
	    var Properties = { 
	        width: parseInt(ComputedElementStyle.getPropertyValue("width")),
	        height: parseInt(ComputedElementStyle.getPropertyValue("height")),
	        padding: {
	            top: parseInt(ComputedElementStyle.getPropertyValue("padding-top")),
	            right: parseInt(ComputedElementStyle.getPropertyValue("padding-right")),
	            bot: parseInt(ComputedElementStyle.getPropertyValue("padding-bottom")),
	            left: parseInt(ComputedElementStyle.getPropertyValue("padding-left"))
	        },
	        margin:{
	            top: parseInt(ComputedElementStyle.getPropertyValue("margin-top")),
	            right: parseInt(ComputedElementStyle.getPropertyValue("margin-right")),
	            bot: parseInt(ComputedElementStyle.getPropertyValue("margin-bottom")),
	            left: parseInt(ComputedElementStyle.getPropertyValue("margin-left"))
	        } 
	    };
	    var DiffValues = { 
	        width: (options['width'] != null) ? (options['width'] - Properties['width']) : 0,
	        height: (options['height'] != null) ? (options['height'] - Properties['height']) : 0,
	        padding: {
	            top: (options['padding'] && options['padding']['top']!=null) ? options['padding']['top'] - Properties['padding']['top'] : 0,
	            right: (options['padding'] && options['padding']['right']!=null) ? options['padding']['right'] - Properties['padding']['right'] : 0,
	            bot: (options['padding'] && options['padding']['bot']!=null) ? options['padding']['bot'] - Properties['padding']['bot'] : 0,
	            left: (options['padding'] && options['padding']['left']!=null) ? options['padding']['left'] - Properties['padding']['left'] : 0
	        },
	        margin:{
	            top: (options['margin'] && options['margin']['top'] != null) ? options['margin']['top'] - Properties['margin']['top'] : 0,
	            right: (options['margin'] && options['margin']['right'] != null) ? options['margin']['right'] - Properties['margin']['right'] : 0,
	            bot: (options['margin'] && options['margin']['bot'] != null) ? options['margin']['bot'] - Properties['margin']['bot'] : 0,
	            left: (options['margin'] && options['margin']['left'] != null) ? options['margin']['left'] - Properties['margin']['left'] : 0
	        }
	    };
	    var beginTime = new Date().getTime(); 
	    var sinceBeginTime;
	    var progressFactor; 
	    
	    animationTime = (animationTime != null) ? animationTime : 250;
	    AttrElementStyle.overflow = "hidden";
	    
	    timer = setInterval(function () {
	        sinceBeginTime = new Date().getTime() - beginTime;

	        if (sinceBeginTime < animationTime) {
	            progressFactor = sinceBeginTime / animationTime;
	            AttrElementStyle.width = (Properties['width'] + DiffValues['width'] * progressFactor) + "px";
	            AttrElementStyle.height = (Properties['height'] + DiffValues['height'] * progressFactor) + "px";
	            AttrElementStyle.padding =
	                (Properties['padding']['top'] + DiffValues['padding']['top'] * progressFactor) + "px " +
	                (Properties['padding']['right'] + DiffValues['padding']['right'] * progressFactor) + "px " +
	                (Properties['padding']['bot'] + DiffValues['padding']['bot'] * progressFactor) + "px " +
	                (Properties['padding']['left'] + DiffValues['padding']['left'] * progressFactor) + "px";
	            AttrElementStyle.margin = 
	                (Properties['margin']['top'] + DiffValues['margin']['top'] * progressFactor) + "px " +
	                (Properties['margin']['right'] + DiffValues['margin']['right'] * progressFactor) + "px " +
	                (Properties['margin']['bot'] + DiffValues['margin']['bot'] * progressFactor) + "px " +
	                (Properties['margin']['left'] + DiffValues['margin']['left'] * progressFactor) + "px";
	        } else {
	            AttrElementStyle.width = options['width'] + "px";
	            AttrElementStyle.height = options['height'] + "px";

	            AttrElementStyle.padding =
	                (Properties['padding']['top'] + DiffValues['padding']['top']) + "px " +
	                (Properties['padding']['right'] + DiffValues['padding']['right']) + "px "+
	                (Properties['padding']['bot'] + DiffValues['padding']['bot']) + "px " +
	                (Properties['padding']['left'] + DiffValues['padding']['left']) + "px";
	            AttrElementStyle.margin =
	                (Properties['margin']['top'] + DiffValues['margin']['top']) + "px " +
	                (Properties['margin']['right'] + DiffValues['margin']['right']) + "px " +
	                (Properties['margin']['bot'] + DiffValues['margin']['bot']) + "px " +
	                (Properties['margin']['left'] + DiffValues['margin']['left']) + "px";

	            clearInterval( timer ); 

	            if ( callback != null ) callback(Properties);
	        }
	    }, 15);
	}

	function slideDown (element, animationTime, callback) {
	    var AttrElementStyle = element.style;
	    var ComputedElementStyle = window.getComputedStyle(element, null);
	    
	    AttrElementStyle.display = "block";
	    
	    var options = {
	    	width: parseInt( ComputedElementStyle.getPropertyValue("width")),
	    	height: parseInt( ComputedElementStyle.getPropertyValue("height")),
	   	 	padding: {
	        	top: parseInt(ComputedElementStyle.getPropertyValue("padding-top")),
	        	bot: parseInt(ComputedElementStyle.getPropertyValue("padding-bottom"))
	        },
	    	margin: {
	        	top: parseInt(ComputedElementStyle.getPropertyValue("margin-top")),
	        	bot: parseInt(ComputedElementStyle.getPropertyValue("margin-bottom"))
	        } 
	    };

	    AttrElementStyle.height = "0";
	    AttrElementStyle.paddingTop = "0";
	    AttrElementStyle.paddingBottom = "0";
	    AttrElementStyle.marginTop = "0";
	    AttrElementStyle.marginBottom = "0";
	    
	    morph(element, options, animationTime, function () { 
	        AttrElementStyle.width = "";
	        AttrElementStyle.height = "";
	        AttrElementStyle.padding = "";
	        AttrElementStyle.margin = "";

	        element.style.display = 'block';

	        if (callback) callback();
	    });
	}

	function slideUp (element, animationTime, callback) {
		var options = {
            height: 0,
            padding: {
                top: 0,
                bot: 0
            },
            margin: {
                top: 0,
                bot: 0
            }
        };

	    morph(element, options, animationTime,  function (Properties) {
            var AttrElementStyle = element.style;

            AttrElementStyle.width = "";
            AttrElementStyle.height = "";
            AttrElementStyle.padding = "";
            AttrElementStyle.margin = "";
            element.style.display = 'none';

        	if (callback) callback();
	    });
	}
