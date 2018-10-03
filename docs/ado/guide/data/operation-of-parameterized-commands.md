---
title: 參數化命令的作業 |Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
helpviewer_keywords:
- data shaping [ADO], parameterized commands
- parameterized commands [ADO]
ms.assetid: 4fae0d54-83b6-4ead-99cc-bcf532daa121
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 7d2d2f8fce7b70c760707bd0d384ffa9b72f7a1d
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/01/2018
ms.locfileid: "47751766"
---
# <a name="operation-of-parameterized-commands"></a>參數化命令的作業
如果您正在使用大型的子系**資料錄集**，特別是相較於父代的大小**資料錄集**，但需要存取只有少數子章節中，您可能會發現它使用更有效率參數化的命令。  
  
 A*非參數化命令*擷取整個父系和子系**資料錄集**將的章節資料行附加至其父代，然後指派每個父資料列的相關的子章節的參考.  
  
 A*參數化命令*擷取整個父代**資料錄集**，但擷取的一章**資料錄集**章節資料行存取時。 這項差異，在擷取策略可以產生顯著的效能效益。  
  
 例如，您可以指定下列作業：  
  
```  
SHAPE {SELECT * FROM customer}   
   APPEND ({SELECT * FROM orders WHERE cust_id = ?}   
   RELATE cust_id TO PARAMETER 0)  
```  
  
 父和子資料表有資料行名稱中常見的 cust_id *。* *子命令*具有"？"預留位置，在 RELATE 子句參考 (也就是"...參數 0"）。  
  
> [!NOTE]
>  參數子句僅屬於圖形命令語法。 它所關聯的其中一個 ADO[參數](../../../ado/reference/ado-api/parameter-object.md)物件或[參數](../../../ado/reference/ado-api/parameters-collection-ado.md)集合。  
  
 參數化的圖形命令執行時，會發生下列情況：  
  
1.  *父命令*會執行並傳回父代**資料錄集**Customers 資料表中。  
  
2.  章節資料行附加至父代**資料錄集**。  
  
3.  存取父資料列的章節資料行時，*子命令*使用 customer.cust_id 的值做為參數的值來執行。  
  
4.  步驟 3 中建立的資料提供者資料列中的所有資料列會用來填入子系**資料錄集**。 在此範例中，這會是其 cust_id 等於 customer.cust_id 值的 「 訂單 」 資料表中的所有資料列。 根據預設，子系**Recordset**s 會快取在用戶端到父系的所有參考**資料錄集**會釋出。 若要變更此行為，將**Recordset** [動態屬性](../../../ado/reference/ado-api/ado-dynamic-property-index.md)**快取子資料列**到**False**。  
  
5.  擷取的子資料列的參考 (也就是子系的章節**Recordset**) 放在目前的資料列的父代的章節資料行**資料錄集**。  
  
6.  存取另一個資料列的章節資料行時，會重複步驟 3 – 5。  
  
 **快取子資料列**動態屬性設定為 **，則為 True**預設。 快取行為，會根據查詢的參數值而有所不同。 在具有單一參數，子查詢**資料錄集**給定的參數值將會快取之間值的子系的要求。 下列程式碼示範：  
  
```  
SCmd = "SHAPE {select * from customer} " & _  
         "APPEND({select * from orders where cust_id = ?} " & _  
         "RELATE cust_id TO PARAMETER 0) AS chpCustOrder"  
Rst1.Open sCmd, Cnn1  
Set RstChild = Rst1("chpCustOrder").Value  
Rst1.MoveNext      ' Next cust_id passed to Param 0, & new rs fetched   
                   ' into RstChild.  
Rst1.MovePrevious  ' RstChild now holds cached rs, saving round trip.  
```  
  
 在具有兩個或多個參數的查詢，只有當所有參數值都符合快取的值，會使用快取子系。  
  
## <a name="parameterized-commands-and-complex-parent-child-relations"></a>參數化的命令和複雜的父代子關聯性  
 除了使用參數化的命令，以改善效能的等聯結 （equi-join） 型別階層架構，參數化的命令可用來支援更複雜的父子式關聯性。 例如，假設兩個資料表的小小的聯盟資料庫： 其中一個小組 （team_id、 team_name） 和其他的遊戲 （日期、 home_team、 visiting_team） 所組成。  
  
 使用非參數化的階層，沒有任何方法可以與小組及遊戲的資料表的方式相關的子系**資料錄集**每個小組包含其完整的排程。 您可以建立包含主排程或 road 排程，但不是能兩者都包含的章節。 這是因為 RELATE 子句會限制您的表單的父子式關聯性 (pc1 = cc1) AND (pc2 = pc2)。 因此，如果您的命令包含"RELATE team_id TO home_team，team_id TO visiting_team 」，您會取得的遊戲，小組已播放本身。 您想要為"(team_id=home_team) 或者 (team_id = visiting_team) 」，但 Shape 提供者不支援 OR 子句。  
  
 若要取得所要的結果，您可以使用參數化的命令。 例如：  
  
```  
SHAPE {SELECT * FROM teams}   
APPEND ({SELECT * FROM games WHERE home_team = ? OR visiting_team = ?}   
        RELATE team_id TO PARAMETER 0,   
               team_id TO PARAMETER 1)   
```  
  
 此範例會利用 SQL WHERE 子句，獲得您需要更大的彈性。  
  
> [!NOTE]
>  當使用 WHERE 子句，參數可以不使用 SQL 資料類型為 text、 ntext 和 image 或會產生錯誤，包含下列描述： `Invalid operator for data type`。  
  
## <a name="see-also"></a>另請參閱  
 [資料成形範例](../../../ado/guide/data/data-shaping-example.md)   
 [正式 Shape 文法](../../../ado/guide/data/formal-shape-grammar.md)   
 [一般 Shape 命令](../../../ado/guide/data/shape-commands-in-general.md)
