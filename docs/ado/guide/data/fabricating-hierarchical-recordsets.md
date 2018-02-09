---
title: "Fabricating 階層式資料錄集 |Microsoft 文件"
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: ado
ms.technology:
- drivers
ms.custom: 
ms.date: 01/19/2017
ms.reviewer: 
ms.suite: sql
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- Recordset fabrication [ADO]
- hierarchical Recordsets [ADO]
- fabricating hierarchical Recordsets [ADO]
- data shaping [ADO], hierarchical Recordsets
ms.assetid: a584e642-a4a3-418e-bc20-3aff81a5625a
caps.latest.revision: 
author: MightyPen
ms.author: genemi
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: dd8c5c97983fbfa0cbf10f302f992c1bd6c9a59f
ms.sourcegitcommit: acab4bcab1385d645fafe2925130f102e114f122
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 02/09/2018
---
# <a name="fabricating-hierarchical-recordsets"></a>Fabricating 階層式資料錄集
下列範例示範如何使用資料的形式來定義資料行的父系、 子群組和孫系文法由此沒有基礎資料來源的階層式資料錄集**資料錄集**。  
  
 要由此階層式**資料錄集**，您必須指定[Microsoft Data Shaping Service 的 OLE DB （ADO 服務提供者）](../../../ado/guide/appendixes/microsoft-data-shaping-service-for-ole-db-ado-service-provider.md) (MSDataShape)，而且您可以指定 NONE 中的資料提供者值連接字串參數的[開啟](../../../ado/reference/ado-api/open-method-ado-connection.md)方法[連接](../../../ado/reference/ado-api/connection-object-ado.md)物件。 如需詳細資訊，請參閱[所需的提供者資料成形](../../../ado/guide/data/required-providers-for-data-shaping.md)。  
  
```  
Dim cn As New ADODB.Connection  
Dim rsCustomers As New ADODB.Recordset  
  
cn.Open "Provider=MSDataShape;Data Provider=NONE;"  
  
strShape = _  
"SHAPE APPEND NEW adInteger AS CustID," & _  
            " NEW adChar(25) AS FirstName," & _  
            " NEW adChar(25) AS LastName," & _  
            " NEW adChar(12) AS SSN," & _  
            " NEW adChar(50) AS Address," & _  
         " ((SHAPE APPEND NEW adChar(80) AS VIN_NO," & _  
                        " NEW adInteger AS CustID," & _  
                        " NEW adChar(20) AS BodyColor, " & _  
                     " ((SHAPE APPEND NEW adChar(80) AS VIN_NO," & _  
                                    " NEW adChar(20) AS Make, " & _  
                                    " NEW adChar(20) AS Model," & _  
                                    " NEW adChar(4) AS Year) " & _  
                        " AS VINS RELATE VIN_NO TO VIN_NO))" & _  
            " AS Vehicles RELATE CustID TO CustID) "  
  
rsCustomers.Open strShape, cn, adOpenStatic, adLockOptimistic, -1  
```  
  
 只要**資料錄集**已傳遞，它可以是填入、 操作，或保存至檔案。  
  
## <a name="see-also"></a>另請參閱  
 [存取資料列中的階層式資料錄集](../../../ado/guide/data/accessing-rows-in-a-hierarchical-recordset.md)   
 [型式圖形文法](../../../ado/guide/data/formal-shape-grammar.md)   
 [提供者所需的資料成形](../../../ado/guide/data/required-providers-for-data-shaping.md)   
 [圖形 APPEND 子句](../../../ado/guide/data/shape-append-clause.md)   
 [一般 Shape 命令](../../../ado/guide/data/shape-commands-in-general.md)
