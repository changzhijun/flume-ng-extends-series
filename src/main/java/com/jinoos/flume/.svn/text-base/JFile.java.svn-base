package com.jinoos.flume;

 

import java.io.BufferedReader;  
import java.io.BufferedWriter;  
import java.io.FileInputStream;  
import java.io.FileOutputStream;  
import java.io.FileWriter;  
import java.io.IOException;  
import java.io.InputStreamReader;  
import java.io.OutputStreamWriter;  
import java.io.PrintWriter;  
import java.util.ArrayList;  
import java.util.Arrays;  
  
/** 
 * 提供了一些"能让你将文本文件当作字符串来读写"的static方法。此外，你还可以创建一个 
 * "会把文件的内容逐行存入ArrayList的"TextFile类，这样在处理文件的时候，就能使用 
 * ArrayList的功能了。 
 */  
public class JFile extends ArrayList {  
    /** 
     * 读取指定的文件到内存中 
     * @param fileName 文件名 
     * @return 将整个文件内容以字符串返回 
     * @throws IOException String 
     */  
    public static String read(String fileName) throws IOException {  
        return read(fileName, System.getProperty("file.encoding"));  
    }  
  
    /** 
     *  
     * 以特定的编码方式读取指定的文件到内存中 
     * @param fileName 文件名 
     * @param encoding 编码方式 
     * @return 将整个文件内容以字符串返回 
     * @throws IOException String 
     */  
    public static String read(String fileName, String encoding) throws IOException {  
        String lineSeparator = System.getProperty("line.separator");  
        StringBuffer sb = new StringBuffer();  
        BufferedReader in = new BufferedReader(new InputStreamReader(new FileInputStream(  
                fileName), encoding));  
        String s;  
        while ((s = in.readLine()) != null) {  
            sb.append(s);  
            sb.append(lineSeparator);  
        }  
        in.close();  
        return sb.toString();  
    }  
    
    /** 
     *  
     * 以特定的编码方式读取指定的文件到内存中 
     * @param fileName 文件名 
     * @param encoding 编码方式 
     * @return 将整个文件内容以字符串返回 
     * @throws IOException String 
     */  
    public static ArrayList<String> readline(String fileName, String encoding) throws IOException { 
    	ArrayList<String> lines = new ArrayList<String>();
    	lines.clear();
         
        StringBuffer sb = new StringBuffer();  
        BufferedReader in = new BufferedReader(new InputStreamReader(new FileInputStream(  
                fileName), encoding));  
        String s;  
        while ((s = in.readLine()) != null) {  
             lines.add(s);
        }  
        in.close();  
        return lines;  
    }
  
    /** 
     * 把文本写入文件中 
     * @param fileName 文件名 
     * @param text 要写的文本 
     * @throws IOException void 
     */  
    public static void write(String fileName, String text) throws IOException {  
        write(fileName, text, System.getProperty("file.encoding"));  
    }  
  
    /** 
     *  
     * 把文本以指定的编码方式写入文件中 
     * @param fileName 文件名 
     * @param text 要写的文本 
     * @param encoding 编码方式 
     * @throws IOException void 
     */  
    public static void write(String fileName, String text, String encoding)  
            throws IOException {  
  
        PrintWriter out = new PrintWriter(new BufferedWriter(new OutputStreamWriter(  
                new FileOutputStream(fileName), encoding)));  
        out.print(text);  
        out.close();  
    }  
  
    /** 
     * 将指定的文件读出后以行为单位存入ArrayList中 
     * @param fileName 文件名 
     * @throws IOException 
     */  
    public JFile(String fileName) throws IOException {  
        super(Arrays.asList(read(fileName).split(System.getProperty("line.separator"))));  
    }  
  
    /** 
     * 将ArrayList中处理过后的文件写回到指定的文件中 
     * @param fileName 文件名 
     * @throws IOException void 
     */  
    public void write(String fileName) throws IOException {  
        PrintWriter out = new PrintWriter(new BufferedWriter(new FileWriter(fileName)));  
        for (int i = 0; i < size(); i++)  
            out.println(get(i));  
        out.close();  
    }  
  
    public static void main(String[] args) throws Exception {  
        String file = read("D:/program/eclipse/changzhijun/flurry/src/com/jfile.java", "UTF-8");  
        write("src/test.txt", file);  
        JFile text = new JFile("src/test.txt");  
        text.write("src/test2.txt");  
        for (int i = 0; i < text.size(); i++) {  
            System.out.println(text.get(i));  
        }  
    }  
}
