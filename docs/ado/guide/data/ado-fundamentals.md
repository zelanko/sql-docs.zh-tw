---
title: ADO 基本概念 |Microsoft 文件
ms.prod: sql
ms.prod_service: drivers
ms.service: ''
ms.component: ado
ms.technology:
- drivers
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.suite: sql
ms.tgt_pltfrm: ''
ms.topic: conceptual
ms.assetid: d6a66928-e68f-4c38-b87a-838c5de50a28
caps.latest.revision: 10
author: MightyPen
ms.author: genemi
manager: craigg
ms.workload: On Demand
ms.openlocfilehash: 54e829ed3c28702144c64c49a9bd425e6488e5d7
ms.sourcegitcommit: bb044a48a6af9b9d8edb178dc8c8bd5658b9ff68
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/18/2018
---
# <a name="ado-fundamentals"></a>ADO 基本概念
ADO 提供開發人員一種功能強大的邏輯物件模型以程式設計方式存取、 編輯和更新資料，從各種不同的資料來源透過 OLE DB 系統介面。 ADO 最常見的使用是查詢關聯式資料庫中資料表或資料表，請擷取和結果顯示在應用程式，並可能讓使用者進行變更和儲存的資料。 其他的工作包括下列各項：  
  
-   查詢資料庫使用 SQL，以及顯示結果。  
  
-   透過網際網路存取的檔案存放區中的資訊。  
  
-   操作訊息和資料夾中的電子郵件系統。  
  
-   將資料從資料庫中儲存成 XML 檔案。  
  
-   執行命令與 XML 描述，和擷取 XML 資料流。  
  
-   將資料儲存到二進位檔或 XML 資料流。  
  
-   允許使用者檢視及變更資料庫資料表中的資料。  
  
-   建立及重複使用參數化資料庫命令。  
  
-   執行預存程序。  
  
-   動態建立彈性的結構，名為**資料錄集**、 可保存、 瀏覽，及操作資料。  
  
-   執行交易式資料庫作業。  
  
-   篩選和排序準則執行階段為基礎的資料庫資訊的本機副本。  
  
-   建立和操作資料庫中的階層式結果。  
  
-   繫結資料庫欄位資料感知的元件。  
  
-   建立遠端，中斷連接**資料錄集**。  
  
 ADO 會公開各種不同的選項和設定來提供這種彈性。 因此，務必了解如何使用 ADO 應用程式中，分解成可管理的片段您目標的每個需要有系統的方法。  
  
 使用 ADO 的大多數應用程式中所涉及的四個主要作業： 取得資料、 檢查資料、 編輯資料，以及更新的資料。 這些作業會於本節稍後的更詳細地檢查。  
  
 不過，我們會討論這些詳細資料之前，我們將提供的概觀，ADO 物件模型以及簡單的 ADO 應用程式，這以 Microsoft® Visual Basic® 撰寫，並執行每四個主要的 ADO 作業：  
  
-   [ADO 物件和集合](../../../ado/guide/data/ado-objects-and-collections.md)  
  
-   [HelloData：簡易 ADO 應用程式](../../../ado/guide/data/hellodata-a-simple-ado-application.md)  
  
-   [OLE DB 提供者](../../../ado/guide/data/ole-db-providers-ado.md)  
  
-   [錯誤](../../../ado/guide/data/errors-ado.md)
