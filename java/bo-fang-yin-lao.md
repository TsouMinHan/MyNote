# 播放音樂

音樂要放在 `class` 的資料夾內，程式碼是抓當前 `class` 路徑下的檔案，因為我找到的程式碼是用這樣的方式，我嘗試過使用 `File` 開啟，但格式不對，所以就沒有修改了。

```java
public void playSound(String file) {
		try{	
			AudioInputStream audioInputStream =AudioSystem.getAudioInputStream(this.getClass().getResource(file));

			Clip clip = AudioSystem.getClip();
			clip.open(audioInputStream);
			clip.start();
			Thread.sleep(2500); // plays up to 2.5 seconds of sound before exiting
			clip.close();
		}
		catch(Exception e){
			e.printStackTrace();
			System.out.println(e);
		}
	}

```

## 參考資料

1. [java - UnsupportedAudioFileException with a .wav file - Stack Overflow](https://stackoverflow.com/questions/63061511/unsupportedaudiofileexception-with-a-wav-file)
2. [java - File loading by getClass\(\).getResource\(\) - Stack Overflow](https://stackoverflow.com/questions/14089146/file-loading-by-getclass-getresource)
3. [How to play mp3 files in java using eclipse? \| DaniWeb](https://www.daniweb.com/programming/software-development/threads/475808/how-to-play-mp3-files-in-java-using-eclipse)

