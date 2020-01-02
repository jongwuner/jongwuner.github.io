---
layout:     post
title:      "Spring, Jackson 라이브러리 이해하기"
subtitle:   "Spring에서 JSON사용하는 방법"
date:       2020-01-02 21:20:00
author:     "jjongwuner"
header-img: "img/post-bg-re-vs-ng2.jpg"
header-mask: 0.3
catalog:    true
categories: web
tags:
  - Web
  - Spring
  - JSON
---

## JACKSON 라이브러리란?

##### pom.xml상에 MAVEN 설정. 

```xml
<properties>
    <jackson.version>2.9.2</jackson.version>
</properties>
  
<dependencies>       
        <dependency>
            <groupId>com.fasterxml.jackson.core</groupId>
            <artifactId>jackson-databind</artifactId>
            <version>${jackson.version}</version>
        </dependency>
</dependencies>
```



```java
import java.io.IOException; 
import java.util.HashMap; 
import java.util.Map; 
import org.codehaus.jackson.JsonGenerationException; 
import org.codehaus.jackson.JsonParseException; 
import org.codehaus.jackson.map.JsonMappingException; 
import org.codehaus.jackson.map.ObjectMapper; 

public class JsonUtils { 
    private JsonUtils(){} 
    public static Map stringToJsonMap(String json){ 
        return stringToObject(json, HashMap.class); 
    } 
    public static Object stringToJsonClass(String json, Class clazz){ 
        return stringToObject(json, clazz); 
    } 
    public static <T> T stringToObject(String jsonString, Class<T> valueType){ 
        try { 
            return new ObjectMapper().readValue(jsonString, valueType); 
        } 
        catch (JsonParseException e) { 
            e.printStackTrace(); 
        } 
        catch (JsonMappingException e) { 
            e.printStackTrace(); 
        } 
        catch (IOException e) { 
            e.printStackTrace(); 
        } 
        return null; 
    } 
    public static String jsonToString(Object jsonObject){ 
        return objectToString(jsonObject); 
    } 
    
    public static String gainJsonToString(Object jsonObject){ 
        return gainJsonToString(jsonObject, true); 
    } 
    public static String gainJsonToString(Object jsonObject, boolean resultAddFlag){ 
        if(resultAddFlag){ 
            Map m = new HashMap(); 
            m.put("result", jsonObject); 
            return objectToString(m); 
        }
        else{ 
            return objectToString(jsonObject); 
        } 
    } 
    public static String objectToString(Object json) { 
        ObjectMapper om = new ObjectMapper(); 
        try { 
            return om.writeValueAsString(json); 
        } 
        catch (JsonGenerationException e) { 
            e.printStackTrace(); 
        } 
        catch (JsonMappingException e) {
            e.printStackTrace(); 
        } 
        catch (IOException e) { 
            e.printStackTrace(); 
        } 
        return ""; 
    } 
    public static String callbackObjectToString(String callback , Object json){ 
        String reval = objectToString(json); 
        
        if(!"".equals(callback)){ 
            reval = callback+"("+reval+")"; 
        } 
        return reval; 
    } 
}


```





## References

- [JACKSON 사용법 (1) ](https://www.lesstif.com/pages/viewpage.action?pageId=24445183)

- [JACKSON 사용법 (2)]([https://unabated.tistory.com/entry/JAVA-JSON-%EB%9D%BC%EC%9D%B4%EB%B8%8C%EB%9F%AC%EB%A6%AC-Jackson-%EC%82%AC%EC%9A%A9%EB%B2%95](https://unabated.tistory.com/entry/JAVA-JSON-라이브러리-Jackson-사용법))

- [JSON <-> HashMap (1)](https://mkil.tistory.com/358)
- [JSON <-> HashMap (2)](https://wckhg89.github.io/archivers/understanding_jackson)

- [POSTMAN을 통해 REST-API TEST (1) ](https://rwd337.tistory.com/173)