# 輸出 jar

**使用 gradle 專案時，不要用 eclipse 內建的方式輸出，在開發時，導入相關 jar 的相依性可能在內建的一些設定檔中沒有儲存，所以輸出後很有可能會發生 NoClassDeFoundError 的錯誤，這問題花了我好幾個小時解決呀。**  


**所以使用 gradle 輸出 jar**  


**若出現中文亂碼問題**  


{% code title="build.gradle" %}
```java
compileJava.options.encoding = 'UTF-8'

tasks.withType(JavaCompile) {
    options.encoding = 'UTF-8'
}
```
{% endcode %}



## 參考資料

1. [Build JAVA project and create JAR file using Gradle - YouTube](https://www.youtube.com/watch?v=BwdkyrnJQsg&ab_channel=LynAsSazzad)
2. [java-project-using-gradle/build.gradle at master · lynas/java-project-using-gradle](https://github.com/lynas/java-project-using-gradle/blob/master/build.gradle)
3. [utf 8 - Show UTF-8 text properly in Gradle - Stack Overflow](https://stackoverflow.com/questions/21267234/show-utf-8-text-properly-in-gradle) 

