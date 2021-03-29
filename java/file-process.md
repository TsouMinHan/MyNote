---
description: 紀錄下在工作時使用到一些處理檔案問題的程式碼。
---

# 檔案處理

## 取得目錄底下的資料夾

```java
public static List<Path> getSubdirectory(String pathStr) throws IOException {
    /* 取得該路徑下所有資料夾 */        
    Path path = Paths.get(pathStr);

    List<Path> result;
    try (Stream<Path> walk = Files.walk(path)) {
        result = walk.filter(Files::isDirectory) // isDirectory 可以改其他參數，可以改抓檔案
                .collect(Collectors.toList());
    }

    return result.subList(1, result.size()); // 第一筆會是該路徑本身，所以去除掉
}
```

## 檢查路徑

### 是否為資料夾

```java
public static void checkFolder(String folderName) throws IOException {
    /* 檢查是否有此資料夾，若無則建立 */
    Path f = Paths.get(folderName);

    if(!Files.isDirectory(f)) { 
        File d = new File(folderName);
        d.mkdir();
    }
}
```

### 是否為檔案

```java
public void checkFilePath(String fileName) throws IOException {
    /* 確認路徑檔案是否存在，若否則建立檔案 */
    Path f = Paths.get(fileName);

    if(!Files.isRegularFile(f)) { 
        Files.createFile(f);
    }
}
```

## 寫入檔案

### 寫入 byte 至 txt

```java
public void writeBytesToFile(String fileOutput, byte[] bytes){
    try (FileOutputStream fos = new FileOutputStream(fileOutput)) {
        fos.write(bytes);
    } catch (FileNotFoundException e) {
        // TODO Auto-generated catch block
        e.printStackTrace();
    } catch (IOException e) {
        // TODO Auto-generated catch block
        e.printStackTrace();
    }
}
```

### 寫入字串至 txt

這邊的是一般編碼模式，若輸入中文打開檔案時會是亂碼。

```java
public void writeStringToFile(String path, String content) throws IOException {    
    Files.write(Paths.get(path), content.getBytes());
}
```

### 以 utf-8 編碼方式寫入。

```java
private void writeStringToFile(String path, String content) throws IOException {    
    try (BufferedWriter writer = Files.newBufferedWriter(Paths.get(path), StandardCharsets.UTF_8)) {
        writer.append(content);

    } catch (IOException e) {
        e.printStackTrace();
    }
}
```

## 讀取檔案

### 從 txt 讀取字串

一般編碼方式讀取，所以無法讀取 utf-8。

```java
public String readStringFromFile(String path) throws IOException {
    return Files.readString(Path.of(path));
}
```

## 刪除資料夾

```java
private boolean deleteDir(File dir) {
    if (!dir.exists()) 
        return false;

    if (dir.isDirectory()) {
        String[] childrens = dir.list();

        for (String child : childrens) {
            boolean success = deleteDir(new File(dir, child));
            if (!success) return false;
        }
    }

    return dir.delete();
}
```

