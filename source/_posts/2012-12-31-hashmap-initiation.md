---
title: HashMap，根据key，value排序和HashMap在声明时初始化
tags:
  - Hashmap
  - Java
url: archives/693.html
id: 693
categories:
  - Default Category
date: 2012-12-31 20:32:31
---




```
/声明的时候初始化      
HashMap hashMap = new HashMap(){
{
      put("a", 1);
      put("b", 3);
      put("c", 2);
       }
}; 
//sorted by value
ArrayList<Map.Entry> l = new ArrayList<Map.Entry>(hashMap.entrySet());    
Collections.sort(l, new Comparator<Map.Entry>() {    
     public int compare(Map.Entry o1, Map.Entry o2) {    
          return o1.getValue().compareTo(o2.getValue())  ;  
      }    
});  
for(Map.Entry e : l) {  
      System.out.println(e.getKey() + "::::" + e.getValue());  
}
//sorted by key
l = new ArrayList<Map.Entry>(hashMap.entrySet());    
Collections.sort(l, new Comparator<Map.Entry>() {    
     public int compare(Map.Entry o1, Map.Entry o2) {    
         return o1.getKey().compareTo(o2.getKey());    
    }    
});  
for(Map.Entry e : l) {  
     System.out.println(e.getKey() + "::::" + e.getValue());  
}        
//sorted by key，利用treeMap的特性
TreeMap treeMap= new TreeMap(hashMap);
for(Iterator iterator=treeMap.keySet().iterator();iterator.hasNext();) {
     String temp=iterator.next();
     System.out.println(temp + "::::" + treeMap.get(temp));  
}
```

