---
layout: post
title: itext写word并实现下载
date: 2013-10-08 16:56
categories: [java, 工具]
tags: []
---

```html
<dependency>
			<groupId>com.lowagie</groupId>
			<artifactId>itext</artifactId>
			<version>4.2.1</version>
		</dependency>
		
		
```



```java
private void writeDoc(Unit unit, int year,List<TaskIndicant> oneTaskIndicants,List<TaskIndicant> twoTaskIndicants,List<TaskIndicant> threeTaskIndicants ,List<TaskIndicant> allTwoTaskIndicants,String filePath) throws IOException, DocumentException {
		Document document = new Document(PageSize.A4, 36, 72, 108, 120);
		File file=new File(filePath);
		Files.createParentDirs(file);
		RtfWriter2.getInstance(document,new FileOutputStream(file));
		document.open();
		
		// 设置中文字体
		BaseFont bfChinese = null;
		bfChinese = BaseFont.createFont("STSongStd-Light", "UniGB-UCS2-H",BaseFont.NOT_EMBEDDED);
		// 标题字体风格
		Font titleFont = new Font(bfChinese, 18, Font.BOLD);
		// 正文字体风格
		Font contextFont = new Font(bfChinese, 11, Font.NORMAL);
		Font parTitle = new Font(bfChinese, 14, Font.BOLD);
		Font par2Title = new Font(bfChinese, 13, Font.BOLD);
		Font par3Title = new Font(bfChinese, 12,Font.BOLD);
		
		//List<TaskIndicant> allTwoTaskIndicants = twoTaskIndicants;
		
		Paragraph bh = new Paragraph("编号：\n\n\n");
		bh.setAlignment(Element.ALIGN_LEFT);
		bh.setFont(parTitle);
		document.add(bh);
		
		
		Paragraph p = new Paragraph(unit.getName() + year + "年度任务目标书");
		p.setAlignment(Element.ALIGN_CENTER);
		p.setFont(titleFont);
		document.add(p);
		Paragraph paragraph = new Paragraph();
		// 设置段距
		// paragraph.setSpacingAfter(10);
		paragraph.setSpacingBefore(12);

		paragraph.setAlignment(Element.ALIGN_LEFT);
		paragraph.setFirstLineIndent(20);
		Chunk chunk = new Chunk();
		chunk.append("根据学校办学目标及：" + year + "年度工作计划，结合你单位的实际，经学校研究决定，现下达你单位" + year
				+ "年度工作目标任务如下。除此之外，还需按质按量完成学校规定和安排的其他任务，并作为基本工作任务进行考核。");
		chunk.setFont(contextFont);
		paragraph.add(chunk);
		document.add(paragraph);
		document.getPageNumber();
		
		Paragraph p1 =new Paragraph("一级指标",parTitle);
		p1.setAlignment(Element.ALIGN_CENTER);
		p1.setFont(titleFont);
		Cell cell1 = new Cell(p1);
		
		
		Paragraph p2 =new Paragraph("二级指标",parTitle);
		p2.setAlignment(Element.ALIGN_CENTER); 
		p2.setFont(titleFont);
		Cell cell2 = new Cell(p2);
		
		Paragraph p3 =new Paragraph("指标说明",parTitle);
		p3.setAlignment(Element.ALIGN_CENTER); 
		p3.setFont(titleFont);
		Cell cell3 = new Cell(p3);
		
		Paragraph p4 =new Paragraph("本年度核心目标任务",parTitle);
		p4.setAlignment(Element.ALIGN_CENTER); 
		p4.setFont(titleFont);
		Cell cell4 = new Cell(p4);
		
		Paragraph p5 =new Paragraph("年末完成情况",parTitle);
		p5.setAlignment(Element.ALIGN_CENTER); 
		p5.setFont(titleFont);
		Cell cell5 = new Cell(p5);
		
		Paragraph p6 =new Paragraph("得分",parTitle);
		p6.setAlignment(Element.ALIGN_CENTER); 
		p6.setFont(titleFont);
		Cell cell6 = new Cell(p6);
		
		cell1.setUseAscender(true); 
		cell1.setVerticalAlignment(Cell.ALIGN_MIDDLE); 
        cell1.setHorizontalAlignment(Element.ALIGN_CENTER);
        cell1.setHorizontalAlignment(1);
        cell2.setUseAscender(true); 
		cell2.setVerticalAlignment(Cell.ALIGN_MIDDLE); 
        cell2.setHorizontalAlignment(Element.ALIGN_CENTER);
        cell2.setHorizontalAlignment(10);
        cell3.setUseAscender(true); 
		cell3.setVerticalAlignment(Cell.ALIGN_MIDDLE); 
        cell3.setHorizontalAlignment(Element.ALIGN_CENTER);
        cell3.setHorizontalAlignment(10);
        cell4.setUseAscender(true); 
		cell4.setVerticalAlignment(Cell.ALIGN_MIDDLE); 
        cell4.setHorizontalAlignment(Element.ALIGN_CENTER);
        cell4.setHorizontalAlignment(1);
        cell5.setUseAscender(true); 
		cell5.setVerticalAlignment(Cell.ALIGN_MIDDLE); 
        cell5.setHorizontalAlignment(Element.ALIGN_CENTER);
        cell5.setHorizontalAlignment(1);
        cell6.setUseAscender(true); 
		cell6.setVerticalAlignment(Cell.ALIGN_MIDDLE); 
        cell6.setHorizontalAlignment(Element.ALIGN_CENTER);
        cell6.setHorizontalAlignment(1);

        Table table = new Table(3);
        
        table.setWidth(90);
		table.setAlignment(1);
		
		table.setSpacing(0);
		
		table.setPadding(10);
		
		//table.setSpacing(1);
		int[] width = {36,34,18};
		table.setWidths(width);
		table.getDefaultCell().setBorder(Rectangle.NO_BORDER);
		
		Table iTable1 = new Table(3);
		int[] width1 = {13,13,30};
		iTable1.setWidths(width1);
		
		
		Table iTable2 = new Table(1);
		
		//int[] width2 = {40};
		//iTable2.setWidth(40);
		
		Table iTable3 = new Table(2);
		int[] width3 = {16,8};
		iTable3.setWidths(width3);
		
		cell1.setHeader(true);
		cell2.setHeader(true);
		cell3.setHeader(true);
		cell4.setHeader(true);
		cell5.setHeader(true);
		cell6.setHeader(true);
		
		iTable1.addCell(cell1);
        iTable1.addCell(cell2);
        iTable1.addCell(cell3);
        
        iTable2.addCell(cell4);
        
        iTable3.addCell(cell5);
        iTable3.addCell(cell6);
        
        iTable1.endHeaders();
        iTable2.endHeaders();
        iTable3.endHeaders();
		
        
        for(int i=0;i<oneTaskIndicants.size();i++){
	        	TaskIndicant oneTaskIndicant = oneTaskIndicants.get(i);
				// * 添加表头
	        	double score = oneTaskIndicant.getScore();
	        	String sScore = setScore(score);
	        Cell cell = new Cell(new Paragraph(i+1+"."+oneTaskIndicant.getDetail()+"（"+sScore+"分）",par2Title));// 单元格
	        cell.setHeader(true);
	        cell.setVerticalAlignment(Element.ALIGN_CENTER);
	        cell.setHorizontalAlignment(Element.ALIGN_CENTER);
	        cell.setHorizontalAlignment(10);
	        long oneId = oneTaskIndicant.getId();
	        System.out.println(oneId);
	        twoTaskIndicants = this.taskIndicantService.listByFirstTaskIncicant2(oneId);
	        
	        
	        int twoSize = twoTaskIndicants.size();
	        if(twoSize == 0){
		        	twoSize = 1;
		        	cell.setRowspan(twoSize);// 设置表格为行
		        	iTable1.endHeaders();
		        	iTable1.addCell(cell);
		        	iTable1.addCell("");
		        	iTable1.addCell("");
	        }else{
		        	cell.setRowspan(twoSize);// 设置表格为行
		        	iTable1.addCell(cell);
		        	iTable1.endHeaders();
	        }
	        
	        for(int j = 0;j<twoTaskIndicants.size();j++){
				TaskIndicant twoTaskIndicant = twoTaskIndicants.get(j);
				int m = j+1;
				double score1 = twoTaskIndicant.getScore();
				String sScore1 = setScore(score1);
				Paragraph pTwo1 =new Paragraph(i+1+"."+m+""+twoTaskIndicant.getDetail()+"（"+sScore1+"分）",par3Title);
				pTwo1.setAlignment(Element.ALIGN_MIDDLE); 
				Cell cellTwo1 = new Cell(pTwo1);
				cellTwo1.setVerticalAlignment(Element.ALIGN_MIDDLE);
				
				String intro = twoTaskIndicant.getIntro();
				if(intro==null){
					intro = " ";
				}
				Paragraph pTwo2 =new Paragraph(intro,contextFont);
				pTwo2.setAlignment(Element.ALIGN_MIDDLE); 
				Cell cellTwo2 = new Cell(pTwo2);
				cellTwo2.setVerticalAlignment(Element.ALIGN_TOP);
				
				Paragraph pTwo4 =new Paragraph("",contextFont);
				pTwo4.setAlignment(Element.ALIGN_MIDDLE); 
				Cell cellTwo4 = new Cell(pTwo4);
				cellTwo4.setVerticalAlignment(Element.ALIGN_TOP);
				
				Paragraph pTwo5 =new Paragraph("",contextFont);
				pTwo5.setAlignment(Element.ALIGN_MIDDLE); 
				Cell cellTwo5 = new Cell(pTwo5);
				cellTwo5.setVerticalAlignment(Element.ALIGN_TOP);
				
				iTable1.addCell(cellTwo1);
				iTable1.addCell(cellTwo2);
				
				iTable3.addCell(cellTwo4);
				iTable3.addCell(cellTwo5);
				
				/*iTable1.addCell(cellTwo3);
				iTable1.addCell(cellTwo4);
				iTable1.addCell(cellTwo5);*/
	        }
        }
        String threeT = "";
        
        for(int i = 0;i<threeTaskIndicants.size();i++){
	        	TaskIndicant threeTaskIndicant = threeTaskIndicants.get(i);
	        	int j = i+1;
	        	threeT = threeT+"\n"+j+"."+threeTaskIndicant.getDetail();
        }
        String headString = "";
        if(threeTaskIndicants.size()!=0){
        		headString = "一.发展类目标";
        }
        
        Paragraph pTwo3 =new Paragraph(headString+threeT,contextFont);
		pTwo3.setAlignment(Element.ALIGN_MIDDLE); 
		Cell cellTwo3 = null;
		cellTwo3 = new Cell(pTwo3);
		cellTwo3.setVerticalAlignment(Element.ALIGN_TOP);
		cellTwo3.setHeader(true);
		if(allTwoTaskIndicants.size()==0){
			cellTwo3.setRowspan(1);
		}else{
			cellTwo3.setRowspan(allTwoTaskIndicants.size());
		}
		
		iTable2.addCell(cellTwo3);
        
		if(twoTaskIndicants.size()==0){
			iTable1.addCell("");
			iTable1.addCell("");
			iTable1.addCell("");
			//iTable2.addCell("");
			iTable3.addCell("");
			iTable3.addCell("");
		}
		
		
        table.insertTable(iTable1);
        table.insertTable(iTable2);
        table.insertTable(iTable3);
        
        
		document.add(table);
		
		document.add(new Paragraph("\n"));
		
		Chunk chunkLast = new Chunk();
		chunkLast.append("校长（签章）\nXX大学\n年月");
		chunkLast.setFont(contextFont);
		Paragraph lastParagraph = new Paragraph(chunkLast);
		//设置段距
		//paragraph.setSpacingAfter(10);
		lastParagraph.setSpacingBefore(12);
		lastParagraph.setAlignment(Element.ALIGN_RIGHT);
		lastParagraph.setFirstLineIndent(20);
		document.add(lastParagraph);
		
		document.close();
	}
	
	private String setScore(double score){
		String sScore = String.valueOf(score);
		int start = sScore.indexOf(".0");
		if(start != -1){
			sScore = sScore.substring(0, start);
		}
		return sScore;
	}
```
上面是service中的，下面是controller，用来下载的


```java
@RequestMapping(value = "/{year}/{unitId}",method = RequestMethod.GET)
	public void download(@PathVariable int year,@PathVariable long unitId, HttpServletResponse response, HttpServletRequest request) throws IOException, DocumentException{
		String fileName=String.valueOf(System.currentTimeMillis()+".doc");
		this.taskBookService.writeFile(year, unitId, request.getSession().getServletContext().getRealPath(File.separator) + path+ fileName);
		this.setResponse(response);
		File file=new File(request.getSession().getServletContext().getRealPath(File.separator) + path+ fileName);
		this.copyFileToResponse(response, file);
		this.deleteFile(file);
	}
	
	private void deleteFile(File... files){
		for(File file:files){
			if(file.exists()){
				file.delete();
			}
		}
	}
	
	private void setResponse(HttpServletResponse response) {
		response.setContentType("application/msword");
        response.setHeader("Content-Disposition", "attachment; filename=taskbook.doc");
    }
	
    private void copyFileToResponse(HttpServletResponse response, File file) {
        OutputStream to = null;
        try {
            to = response.getOutputStream();
            Files.copy(file, to);
            to.flush();
            response.flushBuffer();
        } catch (IOException e) {
            e.printStackTrace();
        }finally{
	    		if(null!=to){
	    			try {
					to.close();
				} catch (IOException e) {
					e.printStackTrace();
				}
	    		}
        }
    }
```




