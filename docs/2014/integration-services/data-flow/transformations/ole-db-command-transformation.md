---
title: OLE DB 命令轉換 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
f1_keywords:
- sql12.dts.designer.oledbcommandtrans.f1
helpviewer_keywords:
- statements [Integration Services]
- OLE DB Command transformation
ms.assetid: baa6735c-5acf-4759-b077-1216aca16c6c
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: 3a8ffc33de161c71c6f72eebf8616d1e814fb994
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 02/08/2020
ms.locfileid: "62770384"
---
# <a name="ole-db-command-transformation"></a>OLE DB 命令轉換
  OLE DB 命令轉換為資料流程中每個資料列執行 SQL 陳述式。 例如，可以執行在資料庫資料表中插入、更新或刪除資料列的 SQL 陳述式。  
  
 您可以利用下列方式設定 OLE DB 命令轉換：  
  
-   提供轉換為每個資料列執行的 SQL 陳述式。  
  
-   指定 SQL 陳述式逾時之前的秒數。  
  
-   指定預設字碼頁。  
  
 SQL 陳述式通常包含參數。 參數值儲存在轉換輸入的外部資料行內，且將輸入資料行對應到外部資料行會將其同時對應到參數。 例如，若要利用資料列在 **ProductKey** 資料行中的值找到 **DimProduct** 資料表中的資料列，然後予以刪除，您可以將名為 **Param_0** 的外部資料行對應到名為 **ProductKey** 的輸入資料行，然後執行 SQL 陳述式 `DELETE FROM DimProduct WHERE ProductKey = ?`。 OLE DB 命令轉換提供了參數名稱，您無法對它們進行修改。 這些參數名稱為 **Param_0**、 **Param_1**等。  
  
 如果您使用 [進階編輯器]  對話方塊設定 OLE DB 命令轉換，SQL 陳述式中的參數可自動對應到轉換輸入的外部資料行上，按一下 [重新整理]  按鈕可以定義每個參數的特性。 但是，如果 OLE DB 命令轉換使用的 OLE DB 提供者不支援從參數中衍生參數資訊，您必須手動設定外部資料行。 這表示您必須將每個參數的資料行加入轉換的外部輸入，更新資料行名稱以使用類似 **Param_0**的名稱，指定 DBParamInfoFlags 屬性的值，並將包含參數值的輸入資料行對應到外部資料行。  
  
 DBParamInfoFlags 的值代表參數的特性。 例如，值 **1** 指定參數為輸入參數，值 **65** 指定參數為可以包含 Null 值的輸入參數。 該值必須與 OLE DB DBPARAMFLAGSENUM 列舉中的值相符。 如需詳細資訊，請參閱 OLE DB 參考文件集。  
  
 OLE DB 命令轉換包括 `SQLCommand` 自訂屬性。 屬性運算式可以在載入封裝時更新這個屬性。 如需詳細資訊，請參閱 [Integration Services &#40;SSIS&#41; 運算式](../../expressions/integration-services-ssis-expressions.md)、[在封裝中使用屬性運算式](../../expressions/use-property-expressions-in-packages.md)和[轉換自訂屬性](transformation-custom-properties.md)。  
  
 這個轉換有一個輸入、一個規則輸出及一個錯誤輸出。  
  
## <a name="logging"></a>記錄  
 您可以記錄 OLE DB 命令轉換對外部資料提供者執行的呼叫。 您可以使用這項記錄功能，疑難排解 OLE DB 命令轉換對外部資料來源執行的連接和命令。 若要記錄 OLE DB 命令轉換對外部資料提供者執行的呼叫，請啟用封裝記錄，然後在封裝層級選取 [診斷]  事件。 如需詳細資訊，請參閱 [封裝執行的疑難排解工具](../../troubleshooting/troubleshooting-tools-for-package-execution.md)。  
  
## <a name="related-tasks"></a>相關工作  
 您可以使用 [!INCLUDE[ssIS](../../../includes/ssis-md.md)] 設計師或物件模型來設定轉換。 如需使用 [!INCLUDE[ssIS](../../../includes/ssis-md.md)] 設計師來設定轉換的詳細資訊，請參閱  [設定 OLE DB 命令轉換](../../configure-the-ole-db-command-transformation.md)。 如需有關以程式設計方式來設定此轉換的詳細資訊，請參閱《開發人員指南》。  
  
## <a name="see-also"></a>另請參閱  
 [資料流程](../data-flow.md)   
 [Integration Services 轉換](integration-services-transformations.md)  
  
  
