# ReadFileTime
读取视频时长<br>
简而言之，代码如下：<br>

import it.sauronsoftware.jave.Encoder;<br>
import it.sauronsoftware.jave.MultimediaInfo;<br>

import java.io.File;<br>

public class ReadVideo {<br>

	public static void main(String[] args) throws Exception {<br>

		File root = new File("D:\\dvd");<br>
		showAllFiles(root);<br>

	}

	final static void showAllFiles(File dir) throws Exception {
		File[] fs = dir.listFiles();
		for (int i = 0; i < fs.length; i++) {
			String path = fs[i].getAbsolutePath();
			int length = path.length();
			if (path.substring(length - 3, length) .equalsIgnoreCase("mp4") ) {
				File source = new File(path);
				Encoder encoder = new Encoder();
				try {
					MultimediaInfo m = encoder.getInfo(source);
					long ms = m.getDuration()/60000;//分钟
					long ls = m.getDuration()/1000-ms*60;//秒
					System.out.println("此视频时长为:" + ms + "分"+ ls + "秒！");
				} catch (Exception e) {
					e.printStackTrace();
				}
			}
			if (fs[i].isDirectory()) {
				try {
					showAllFiles(fs[i]);
				} catch (Exception e) {
				}
			}
		}
	}
}


