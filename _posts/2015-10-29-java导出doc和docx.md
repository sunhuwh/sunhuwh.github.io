---
layout: post
title: java导出doc和docx
date: 2015-10-29 19:55
categories: [java]
tags: [java, doc, docx, itext]
---
##导出doc，使用itext：
pom.xml中加入：
	<!-- itext -->
	<dependency>
	    <groupId>com.lowagie</groupId>
	    <artifactId>itext</artifactId>
	    <version>2.1.7</version>
	</dependency>
	
	<dependency>
	    <groupId>com.lowagie</groupId>
	    <artifactId>itext-rtf</artifactId>
	    <version>2.1.7</version>
	</dependency>
代码：
	public static void main(String[] args){
	    String outPath+"D:/test.doc";
	    Document document = new Document(PageSize.A4, 36, 72, 108, 120);
	    File file=new File(outPath);
	    RtfWriter2.getInstance(document,new FileOutputStream(file));
	    document.open();
	    createParagraph(document, "xxx");
	    File file = new File("D:/img1.png");
	    BufferedImage buffeImage = ImageIO.read(file);
	    insertImgByAlign(document, file.getPath(), 0, buffeImage.getHeight(), buffeImage.getWidth());
	    document.close();
	    File file = new File(outPath);
	    response.setHeader("Content-Type", "application/msword");
	    String fileName = WebUtil.encodeDownloadFileName(file.getName());
	    response.setHeader("Content-Disposition", "attachment;filename=" + fileName);
	    WebUtil.writeFileToResponse(response, file);
	}
	private void createParagraph(Document document, String text) throws DocumentException, MalformedURLException, IOException{
	    Paragraph bh = new Paragraph(text);
	    bh.setAlignment(Element.ALIGN_LEFT);
	    getImageAligns(text, document);
	}
	/*
	* 插入图片如果在这里修改长和宽，图片的大小还是原来的大小，所以最好先设置图片合适的大小，再插入
	 * @param document 文档对象
	 * @param imgUrl 图片路径 
	 * @param imageAlign 显示位置 
	 * @param height 显示高度 
	 * @param weight 显示宽度 
	 * @throws MalformedURLException 
	 * @throws IOException 
	 * @throws DocumentException 
	 */  
	public void insertImgByAlign(Document document,String imgUrl,int imageAlign,int height,
	int weight) throws MalformedURLException, IOException, DocumentException{  
	    Image img = Image.getInstance(imgUrl);
	    if(img==null)  
	        return;  
	    img.setAlignment(imageAlign);  
	    img.scaleAbsolute(weight,height);  
	    document.add(img);
	}
	
###导出docx
用poi来实现：
	XWPFDocument doc = new XWPFDocument();
	XWPFParagraph citiaoP = doc.createParagraph();
	XWPFRun citiaoR = citiaoP.createRun();
	citiaoR.setText("text");
	try {
	    FileOutputStream out = new FileOutputStream(outPath);
	        doc.write(out);
	    out.close();
	} catch (IOException e) {
	    // TODO Auto-generated catch block
	    e.printStackTrace();
	}
	File file = new File(outPath);
	response.setHeader("Content-Type", "application/msword");
	String fileName = WebUtil.encodeDownloadFileName(file.getName());
	response.setHeader("Content-Disposition", "attachment;filename=" + fileName);
	WebUtil.writeFileToResponse(response, file);
	
	
