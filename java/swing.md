---
description: 雖然 swing 似乎已經過氣，甚至要死掉了，但有用到就還是紀錄一下吧。
---

# Swing

## 取得螢幕大小

```java
Dimension screenSize = Toolkit.getDefaultToolkit().getScreenSize();
int width = (int)screenSize.getWidth();
int height = (int)screenSize.getHeight();
```

## 上傳圖片

### 建立上傳圖片視窗

```java
package Register;

import java.io.File;

import javax.swing.filechooser.FileFilter;

class ImageFilter extends FileFilter {
       public final static String JPEG = "jpeg";
       public final static String JPG = "jpg";
       public final static String GIF = "gif";
       public final static String TIFF = "tiff";
       public final static String TIF = "tif";
       public final static String PNG = "png";

       @Override
       public boolean accept(File f) {
          if (f.isDirectory()) {
             return true;
          }

          String extension = getExtension(f);
          if (extension != null) {
             if (extension.equals(TIFF) ||
                extension.equals(TIF) ||
                extension.equals(GIF) ||
                extension.equals(JPEG) ||
                extension.equals(JPG) ||
                extension.equals(PNG)) {
                return true;
             } else {
                return false;
             }
          }
          return false;
       }

       @Override
       public String getDescription() {
          return "選取圖片";
       }

       public void setCurrentDiretory(File dir) {

       }

       String getExtension(File f) {
          String ext = null;
          String s = f.getName();
          int i = s.lastIndexOf('.');

          if (i > 0 &&  i < s.length() - 1) {
             ext = s.substring(i+1).toLowerCase();
          }
          return ext;
       } 
    }
```

### 點擊按鈕上傳圖片

```java
this.view.getBtnUploadImg().addActionListener(new ActionListener() {
    private JFileChooser photoFileChooser;

    @Override
    public void actionPerformed(ActionEvent e) {
        // TODO Auto-generated method stub
        photoFileChooser = new JFileChooser(System.getProperty("user.dir"));
        photoFileChooser.setBounds(750, 310, 290, 300);
        photoFileChooser.addChoosableFileFilter(new ImageFilter());
        photoFileChooser.setAcceptAllFileFilterUsed(false);

        int option = photoFileChooser.showOpenDialog(new JFrame());

        if(option == JFileChooser.APPROVE_OPTION){                    
            photo = photoFileChooser.getSelectedFile(); // 給予 photo 值，判斷是否有上傳照片

            // 重新設定圖片大小，讓圖片符合顯示的視窗
            ImageIcon imageIcon = new ImageIcon(photo.toString()); // load the image to a imageIcon
            Image image = imageIcon.getImage(); // transform it 
            Image newimg = image.getScaledInstance(288, 375,  java.awt.Image.SCALE_SMOOTH); // scale it the smooth way  
            imageIcon = new ImageIcon(newimg);  // transform it back
            view.getBtnPhotoImg().setIcon(imageIcon);
            }
    }

});
```

