···

Iterator it = mp.entrySet\(\).iterator\(\);  
    while\(it.hasNext\(\)\)  
    Map.Entrypair = \(Map.Entry\)it.next\(\);  
    System.out.println\(pair.getKey\(\) +" = "+ pair.getValue\(\)\);  
     it.remove\(\);// avoids a ConcurrentModificationException  
 }

···



