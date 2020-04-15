---
title: SQLSetConnectOption(可視化狐狸Pro ODBC驅動程式) |微軟文件
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- SQLSetConnectOption function [ODBC], Visual FoxPro ODBC Driver
ms.assetid: 5a35449e-4694-4ee5-9fa1-45d5a8fe7823
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 2af208663f1e91250faad0ca9538b76bcec43b06
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/14/2020
ms.locfileid: "81301499"
---
# <a name="sqlsetconnectoption-visual-foxpro-odbc-driver"></a>SQLSetConnectOption (Visual FoxPro ODBC Driver)
> [!NOTE]  
>  本主題包含 Visual FoxPro ODBC 特定於驅動程式的資訊。 有關此功能的一般資訊,請參閱[ODBC API 參考](../../odbc/reference/syntax/odbc-api-reference.md)下的相應主題。  
  
 支援:部分  
  
 ODBC API 符合性:1 級  
  
 設置控制連接方面的選項。 此函數部分支援:驅動程式支援*fOption*參數的所有值,但不支援*fOption*參數SQL_TXN_ISOLATION的某些*vParam*值。  
  
 下表僅描述具有特定於**SQLSetConnectOption**的 Visual FoxPro ODBC 驅動程式實現的參數。  
  
|*fOption*|備註|  
|---------------|-------------|  
|SQL_AUTOCOMMIT|如果選擇SQL_AUTOCOMMIT_OFF,則應用程式必須顯式提交或回滾[SQLTransact 的](../../odbc/microsoft/sqltransact-visual-foxpro-odbc-driver.md)事務。Visual FoxPro ODBC 驅動程式在完成時不會自動提交可交易聲明。 如果語句是可操作的,則驅動程序確實會啟動事務。|  
|SQL_CURRENT_QUALIFIER|可以是完全限定[的資料庫](../../odbc/microsoft/visual-foxpro-terminology.md)名稱或包含零個或多個[可用表](../../odbc/microsoft/visual-foxpro-terminology.md)的目錄的完全限定路徑。|  
|SQL_LOGINTIMEOUT|返回"驅動程式無法工作"錯誤。|  
|SQL_CURSORS|返回"驅動程式無法工作"錯誤。|  
|SQL_PACKET_SIZE|返回"驅動程式無法工作"錯誤。|  
|SQL_TXN_ISOLATION|驅動程式只允許SQL_TXN_READ_COMMITTED。<br /><br /> 不支援以下*vParams:*<br /><br /> SQL_TXN_READ_UNCOMMITTED<br /><br /> SQL_TXN_REAPEATABLE_READ<br /><br /> SQL_TXN_SERIALIZABLE|  
  
 有關詳細資訊,請參閱*ODBC 程式師參考*中的[SQLSetConnectOption。](../../odbc/reference/syntax/sqlsetconnectoption-function.md)
