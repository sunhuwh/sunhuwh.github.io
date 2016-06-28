---
layout: post
title: SSH的update实现方法
date: 2013-04-08 21:25
categories: [SSH]
tags: []
---
可以利用java的反射机制
UserDaoImpl.java(底层Dao实现)


```java
/**
     * table 表
     * fieldName 字段名
     * fieldValue 字段值
     * desc 顺序或倒序
     * descId 用来标识用什么来顺序或倒序
     */
    public List selete(String fieldName,String fieldValue,String desc,String table,String descId) {  
        String hql;
        
    	if(fieldName == null&desc==null&descId ==null){
        	hql="from "+table;  
        }else if(desc == null&fieldName!=null&descId ==null){
        	hql="from "+table+" where "+fieldName+" = '"+fieldValue+"'";  
        }else if(desc==null&fieldName==null&descId!=null){
        	hql="from "+table+" order by "+ descId;  
        }else if(desc!=null&fieldName==null&descId!=null){
        	hql="from "+table+" order by "+ descId +" "+desc;  
        }else{
        	hql="from "+table+" where "+fieldName+" = '"+fieldValue+"' order by "+ descId+" "+desc;  
        }
        Query query=session.createQuery(hql);  
        List list=query.list();
        
        return list;
            
    }


```java
 /**
     * 修改数据
     * @param obj
     * @param table
     * @param id
     * @param array1 String字段名集合
     * @param array2 String字段值集合
     * @param array3 Integer字段名集合
     * @param array4 Integer字段值集合
     * @param array5 Date字段名集合
     * @param array6 Date字段值集合
     * @return
     */
    public boolean edit(Object obj,String fieldName,String fieldValue,String table,String[] array1,String[] array2,String[] array3,Integer[] array4,String[] array5,Date[] array6){
    	
    	String desc = null;
    	String descId = null;
    	List list = this.selete(fieldName,fieldValue,desc,table,descId);
    	
    	for(int i=0;i<list.size();i++){
			obj = (Object)list.get(i);
			Class model;
			try {//这里我利用上了反射机制
				model = Class.forName("org.cyxl.ssh.entity."+table);
				
				if(array6==null&array4==null){
				
					for(int j =0;j<array1.length;j++){
						
						Method setMethod = model.getMethod("set"+array1[j],String.class);
						setMethod.invoke(obj, array2[j]);
						session.save(obj);
				    	session.beginTransaction().commit();
			    	}
				}else if(array6==null&array2==null){
					for(int j =0;j<array3.length;j++){
						
						Method setMethod = model.getMethod("set"+array3[j],Integer.class);
						setMethod.invoke(obj, array4[j]);
						session.save(obj);
				    	session.beginTransaction().commit();
				    	
			    	}
				}else{
					for(int j =0;j<array5.length;j++){
						
						Method setMethod = model.getMethod("set"+array5[j],Date.class);
						setMethod.invoke(obj, array6[j]);
						session.save(obj);
				    	session.beginTransaction().commit();
			    	}
				}
			} catch (ClassNotFoundException e) {
			// TODO Auto-generated catch block
			e.printStackTrace();
			}
		
			catch (IllegalAccessException e) {
			// TODO Auto-generated catch block
			e.printStackTrace();
			} catch (SecurityException e) {
			// TODO Auto-generated catch block
			e.printStackTrace();
			} catch (NoSuchMethodException e) {
			// TODO Auto-generated catch block
			e.printStackTrace();
			} catch (IllegalArgumentException e) {
				// TODO Auto-generated catch block
				e.printStackTrace();
			} catch (InvocationTargetException e) {
				// TODO Auto-generated catch block
				e.printStackTrace();
			}
    	
    	}
    	
    	return true;
    }
```


	




```
