# ReadFileTime
读取视频时长<br>
简而言之，代码如下：<br>

import it.sauronsoftware.jave.Encoder;
import it.sauronsoftware.jave.MultimediaInfo;

import java.io.File;

public class ReadVideo {

	public static void main(String[] args) throws Exception {

		File root = new File("D:\\dvd");
		showAllFiles(root);

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


