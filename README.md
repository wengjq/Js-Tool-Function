# Js-Tool-Function
一些 js 工具函数及题目

## 去除字符串两端空格
    
    function trim(string) {
      if (!string) {
        return string
      }
      if (string) {
        return string.trim()
      }
      return (string + "").replace(/^[\s\uFEFF\xA0]+|[\s\uFEFF\xA0]+$/g, "");
    }
