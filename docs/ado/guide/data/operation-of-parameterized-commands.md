---
description: 參數化命令的作業
title: 參數化命令的操作 |Microsoft Docs
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
author: rothja
ms.author: jroth
ms.openlocfilehash: 36934de15041ddec97b0cc266a980f4908518a24
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/17/2020
ms.locfileid: "88453100"
---
# <a name="operation-of-parameterized-commands"></a>參數化命令的作業
如果您使用的是大型的子 **記錄集**，特別是與父 **記錄集**的大小相較之下，但只需要存取一些子章節，您可能會發現使用參數化命令會更有效率。  
  
 *非參數化命令*會同時抓取整個父**記錄集和子記錄集**、將章節資料行附加至父系，然後為每個父資料列指派相關子章節的參考。  
  
 *參數化命令*會抓取整個父**記錄集**，但只會在存取章節資料行時，只抓取章節**記錄集**。 這項抓取策略的差異可能會產生顯著的效能優勢。  
  
 例如，您可以指定下列各項：  
  
```  
SHAPE {SELECT * FROM customer}   
   APPEND ({SELECT * FROM orders WHERE cust_id = ?}   
   RELATE cust_id TO PARAMETER 0)  
```  
  
 父資料表和子資料工作表的資料行名稱都是 common， *cust_id*。 *子命令*有 "？" 預留位置，其關聯子句參考 (也就是 ".。。參數 0 ") 。  
  
> [!NOTE]
>  PARAMETER 子句僅適用于 shape 命令語法。 它與 ADO [參數](../../../ado/reference/ado-api/parameter-object.md) 物件或 [Parameters](../../../ado/reference/ado-api/parameters-collection-ado.md) 集合沒有關聯。  
  
 執行參數化圖形命令時，會發生下列情況：  
  
1.  執行 *父命令* ，並傳回 Customers 資料表中的父 **記錄集** 。  
  
2.  將章節資料行附加至父 **記錄集**。  
  
3.  存取父資料列的章節資料行時，會使用 customer 的值來執行 *子命令* 。 cust_id 做為參數的值。  
  
4.  在步驟3中建立的資料提供者資料列集內的所有資料列，都會用來填入子 **記錄集**。 在此範例中，這是 Orders 資料表中的所有資料列，其中 cust_id 等於 customer 的值。 cust_id。 根據預設，子 **記錄集會**在用戶端上快取，直到父 **記錄集** 的所有參考都已釋放為止。 若要變更此行為，請將**記錄集**[動態屬性](../../../ado/reference/ado-api/ado-dynamic-property-index.md)快取**子資料列**設為**False**。  
  
5.  已抓取之子資料列的參考 (也就是，子 **記錄集**) 的章節會放置在父 **記錄集**目前資料列的章節資料行中。  
  
6.  當存取另一個資料列的章節資料行時，會重複步驟3-5。  
  
 預設會將 [快取 **子資料列** 動態] 屬性設定為 **True** 。 快取行為會依據查詢的參數值而有所不同。 在具有單一參數的查詢中，會在具有該值之子系的要求之間快取指定參數值的子 **記錄集** 。 下列程式碼將示範此作業：  
  
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
  
 在具有兩個或多個參數的查詢中，只有當所有參數值都符合快取的值時，才會使用快取的子系。  
  
## <a name="parameterized-commands-and-complex-parent-child-relations"></a>參數化命令和複雜的父子關聯  
 除了使用參數化命令來改善等聯結型別階層的效能之外，參數化命令還可以用來支援更複雜的父子式關聯性。 例如，假設有一個具有兩個數據表的小聯盟資料庫：其中一個是由團隊 (team_id、team_name) 以及比賽 (日期、home_team visiting_team) 。  
  
 使用非參數化階層時，沒有任何方法可將小組和比賽資料表相關聯，讓每個小組的子 **記錄集** 都包含其完整排程。 您可以建立包含主排程或道路排程的章節，但不能同時建立兩者。 這是因為「關聯」子句會將您限制為表單 (test-pc1 = cc1) 和 (pc2 = pc2) 的父子式關聯性。 因此，如果您的命令包含「讓 team_id 的關聯 home_team，team_id visiting_team」，您就只會取得小組自行播放的遊戲。 您想要的是「 (team_id = home_team) 或 (team_id = visiting_team) 」，但圖形提供者不支援或子句。  
  
 若要取得所需的結果，您可以使用參數化命令。 例如：  
  
```  
SHAPE {SELECT * FROM teams}   
APPEND ({SELECT * FROM games WHERE home_team = ? OR visiting_team = ?}   
        RELATE team_id TO PARAMETER 0,   
               team_id TO PARAMETER 1)   
```  
  
 這個範例會利用 SQL WHERE 子句的更大彈性來取得您所需的結果。  
  
> [!NOTE]
>  使用 WHERE 子句時，參數無法使用 text、Ntext 和 image 的 SQL 資料類型，否則會產生包含下列描述的錯誤： `Invalid operator for data type` 。  
  
## <a name="see-also"></a>另請參閱  
 [資料成形範例](../../../ado/guide/data/data-shaping-example.md)   
 [正式式圖形文法](../../../ado/guide/data/formal-shape-grammar.md)   
 [一般 Shape 命令](../../../ado/guide/data/shape-commands-in-general.md)
