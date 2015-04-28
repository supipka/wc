# wc

import java.io.*;
 
/**
 * 统计文本文件的行数，单词书，字节数
 */
class WordCount {
    public static int words = 1;
    public static int lines = 1;
    public static int chars = 0;
 
    public static void wc(InputStream f) throws IOException {
        int c = 0;
        boolean lastNotWhite = false;
        String whiteSpace = " \t\n\r";
        while ((c = f.read()) != -1) {
            chars++;
            if (c == '\n') {
                lines++;
            }
            if (whiteSpace.indexOf(c) != -1) {
                if (lastNotWhite) {
                    words++;
                }
                lastNotWhite = false;
            } else {
                lastNotWhite = true;
            }
        }
    }
 
    public static void main(String args[]) {
        FileInputStream f;
        try {
            if (args.length == 0) { // We're working with stdin
                f = new FileInputStream("c:/123.txt");
                wc(f);
            } else { // We're working with a list of files
                for (int i = 0; i < args.length; i++) {
                    f = new FileInputStream(args[i]);
                    wc(f);
                }
            }
        } catch (IOException e) {
            return;
        }
        System.out.println(lines + "行 " + words + "个单词 " + chars + "个字节");
    }
}
