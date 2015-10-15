package com.jinoos.flume;

import java.io.BufferedReader;
import java.io.File;
import java.io.FileNotFoundException;
import java.io.IOException;
import java.io.RandomAccessFile;
import java.util.ArrayList;
import java.util.HashMap;
import java.util.List;
import java.util.Map;

import org.apache.commons.vfs2.FileObject;
import org.apache.flume.Transaction;
import org.apache.flume.source.AbstractSource;
import org.slf4j.Logger;
import org.slf4j.LoggerFactory;

public class FileSet {
  private static final Logger logger = LoggerFactory.getLogger(FileSet.class);
  private AbstractSource source;
  private FileObject fileObject;
  private BufferedReader bufferedReader;
  private RandomAccessFile rReader;
  private Transaction transaction;
  private List<String> bufferList;
  private Map<String, String> headers;
  private long lastAppendTime;
  private Long seq;
  private File f;
  private String rwfile;

  public FileSet(AbstractSource source, FileObject fileObject)
      throws IOException {
    this.source = source;
    this.fileObject = fileObject;

    this.bufferList = new ArrayList<String>();

    this.f= new File(fileObject.getName().getPath());
    this.rwfile = "./tmp/lines/"+fileObject.getName().getPath().replaceAll("/", "_");

    rReader = new RandomAccessFile(f, "r");

    
    //rReader.seek(f.length());
    rReader.seek(this.readFile());

    bufferList = new ArrayList<String>();
    headers = new HashMap<String, String>();
    logger.debug("FileSet has been created " + fileObject.getName().getPath()+", seek line="+this.readFile());
    this.seq = 0L;
  }
  // opera,changzhijun
  public FileSet(AbstractSource source, FileObject fileObject, boolean isNew)
	      throws IOException {
	    this.source = source;
	    this.fileObject = fileObject;

	    this.bufferList = new ArrayList<String>();

	    this.f= new File(fileObject.getName().getPath());

	    rReader = new RandomAccessFile(f, "r");

	    rReader.seek(0);

	    bufferList = new ArrayList<String>();
	    headers = new HashMap<String, String>();
	    logger.debug("FileSet has been created " + fileObject.getName().getPath());
	    this.seq = 0L;
	  }

  // opera, init fileset  where mv log runtime
  public void dyncInitFileSet() throws IOException
  {
	    this.bufferList = new ArrayList<String>();

	    this.f= new File(fileObject.getName().getPath());

	    rReader = new RandomAccessFile(f, "r");

	    rReader.seek(0);

	    bufferList = new ArrayList<String>();
	    headers = new HashMap<String, String>();
	    logger.debug("FileSet has been created " + fileObject.getName().getPath());
	    this.seq = 0L;
  }
  
  public String readLine() throws IOException {
	   
	  return rReader.readLine();
  }
  // opera, get filelength
  public long getFileLength()
  {
	 // this.f= new File(fileObject.getName().getPath());
	  return f.length();
  }
  // opera
  public long getReaderPos() throws IOException
  {
	  return rReader.getFilePointer();
	  
  }
  // opera
  public void setReaderPos(long pos) throws IOException
  {
	  rReader.seek(pos);
	  this.seq = 0L;
	  
  }
  // opera,changzhijun
  public void writeFile(long line)
  {
	  try {
		 // logger.debug("opera, begin write line="+ line );
		JFile.write(this.rwfile, Long.toString(line));
		logger.debug("opera, file="+this.rwfile+" seek line="+ line );
	} catch (IOException e) {
		e.printStackTrace();
		logger.error("opera, file="+this.rwfile+" seek line="+ line );
	} 
  }
  // opera, changzhijun
  public long readFile()
  {
	  String line = "0";
	try {
		line = JFile.read(this.rwfile).trim();
		  return Long.parseLong(line);
	} catch (IOException e) {
		e.printStackTrace();
		return f.length();
	}
	  
	
  }
  public long getLastAppendTime() {
    return lastAppendTime;
  }

  public void setLastAppendTime(long lastAppendTime) {
    this.lastAppendTime = lastAppendTime;
  }

  public boolean appendLine(String buffer) {
    boolean ret = bufferList.add(buffer);
    if (ret) {
      lastAppendTime = System.currentTimeMillis();
    }

    return ret;
  }

  public int getLineSize() {
    return bufferList.size();
  }

  public StringBuffer getAllLines() {

    StringBuffer sb = new StringBuffer();

    for (int i = 0; i < bufferList.size(); i++) {
      sb.append(bufferList.get(i));
    }
    return sb;
  }

  public void setHeader(String key, String value) {
    headers.put(key, value);
  }

  public String getHeader(String key) {
    headers.get(key);
    return null;
  }

  public void clear() {
    bufferList.clear();
    headers.clear();
  }

  public Map<String, String> getHeaders() {
    return headers;
  }

  public AbstractSource getSource() {
    return source;
  }

  public void setSource(AbstractSource source) {
    this.source = source;
  }

  public List<String> getBufferList() {
    return bufferList;
  }

  public void setBufferList(List<String> bufferList) {
    this.bufferList = bufferList;
  }

  public Transaction getTransaction() {
    return transaction;
  }

  public void setTransaction(Transaction transaction) {
    this.transaction = transaction;
  }

  public FileObject getFileObject() {
    return fileObject;
  }

  public void setFileObject(FileObject fileObject) {
    this.fileObject = fileObject;
  }

  public BufferedReader getBufferedReader() {
    return bufferedReader;
  }

  public void setBufferedReader(BufferedReader bufferedReader) {
    this.bufferedReader = bufferedReader;
  }

  public Long getSeq() {
    return ++seq;
  }

  /*
   * public void setSeq(Long seq) { this.seq = seq; }
   */

}
