https://scotch.io/tutorials/creating-desktop-applications-with-angularjs-and-github-electron
https://github.com/jasimea/ElectronAngular/blob/master/Gulpfile.js
https://github.com/electron/electron-quick-start/blob/master/package.json
import java.io.File;

import javax.swing.filechooser.FileSystemView;



public class HardDiskApplication {
	public static void main(String [] args){
		File[] paths;
		FileSystemView fsv = FileSystemView.getFileSystemView();

		// returns pathnames for files and directory
		paths = File.listRoots();

		// for each pathname in pathname array
		for(File path:paths)
		{
		    // prints file and directory paths
		    System.out.println("Drive Name: "+path);
		    System.out.println("Description: "+fsv.getSystemTypeDescription(path));
		}
		
	}
}
String string_date = "12-December-2012";

SimpleDateFormat f = new SimpleDateFormat("dd-MMM-yyyy");
try {
    Date d = f.parse(string_date);
    long milliseconds = d.getTime();
} catch (ParseException e) {
    e.printStackTrace();
}
/**
 * Contains some methods to list files and folders from a directory
 *
 * @author Loiane Groner
 * http://loiane.com (Portuguese)
 * http://loianegroner.com (English)
 */
public class ListFilesUtil {
    /**
     * List all the files and folders from a directory
     * @param directoryName to be listed
     */
    public void listFilesAndFolders(String directoryName){
        File directory = new File(directoryName);
        //get all the files from a directory
        File[] fList = directory.listFiles();
        for (File file : fList){
            System.out.println(file.getName());
        }
    }
    /**
     * List all the files under a directory
     * @param directoryName to be listed
     */
    public void listFiles(String directoryName){
        File directory = new File(directoryName);
        //get all the files from a directory
        File[] fList = directory.listFiles();
        for (File file : fList){
            if (file.isFile()){
                System.out.println(file.getName());
            }
        }
    }
    /**
     * List all the folder under a directory
     * @param directoryName to be listed
     */
    public void listFolders(String directoryName){
        File directory = new File(directoryName);
        //get all the files from a directory
        File[] fList = directory.listFiles();
        for (File file : fList){
            if (file.isDirectory()){
                System.out.println(file.getName());
            }
        }
    }
    /**
     * List all files from a directory and its subdirectories
     * @param directoryName to be listed
     */
    public void listFilesAndFilesSubDirectories(String directoryName){
        File directory = new File(directoryName);
        //get all the files from a directory
        File[] fList = directory.listFiles();
        for (File file : fList){
            if (file.isFile()){
                System.out.println(file.getAbsolutePath());
            } else if (file.isDirectory()){
                listFilesAndFilesSubDirectories(file.getAbsolutePath());
            }
        }
    }
    public static void main (String[] args){
        ListFilesUtil listFilesUtil = new ListFilesUtil();
        final String directoryLinuxMac ="/Users/loiane/test";
        //Windows directory example
        final String directoryWindows ="C://test";
        listFilesUtil.listFiles(directoryLinuxMac);
    }
}
//https://www.mkyong.com/java/how-to-write-an-object-to-file-in-java/
