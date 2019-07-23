---
title: setResponseBuffering 方法 (SQLServerStatement) |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLServerStatement.setResponseBuffering(String responseBufferingValue)
apilocation:
- SQLServerStatement.setResponseBuffering(String responseBufferingValue)
apitype: Assembly
ms.assetid: 9f489835-6cda-4c8c-b139-079639a169cf
author: MightyPen
ms.author: genemi
ms.openlocfilehash: a55f1d5695c2595b5ea721680fc77f88d13494ed
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MTE75
ms.contentlocale: zh-TW
ms.lasthandoff: 07/15/2019
ms.locfileid: "67973115"
---
# <a name="setresponsebuffering-method-sqlserverstatement"></a>setResponseBuffering 方法 (SQLServerStatement)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  將這個 [SQLServerStatement](../../../connect/jdbc/reference/sqlserverstatement-class.md) 物件的回應緩衝模式設定為 **String full** 或 **adaptive** (不區分大小寫)。  
  
## <a name="syntax"></a>語法  
  
```  
  
public final void setResponseBuffering(java.lang.String value)  
```  
  
#### <a name="parameters"></a>參數  
 *value*  
  
 **String**，包含回應緩衝模式。 有效模式可能是下列其中一個區分大小寫的 String：**full** 或 **adaptive**。  
  
## <a name="exceptions"></a>例外狀況  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>Remarks  
 **adaptive** 會指定在必要時緩衝處理可能的資料下限。  
  
 **full** 會指定在執行階段從伺服器讀取整個結果。  
  
 「自動調整」是 JDBC 驅動程式2.0 和3.0 版中的預設值。 full 是 JDBC 驅動程式2.0 版之前的預設值。  
  
 [setResponseBuffering](../../../connect/jdbc/reference/setresponsebuffering-method-sqlserverstatement.md) 可讓您覆寫目前 [SQLServerStatement](../../../connect/jdbc/reference/sqlserverstatement-class.md) 物件的 **responseBuffering** 連線 **String** 屬性。 如需使用回應緩衝模式的詳細資訊, 請參閱[使用適應性緩衝](../../../connect/jdbc/using-adaptive-buffering.md)。  
  
 如果應用程式指定給 [setResponseBuffering](../../../connect/jdbc/reference/setresponsebuffering-method-sqlserverstatement.md) 方法的參數值無效，則會擲回 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)。  
  
## <a name="see-also"></a>另請參閱  
 [SQLServerStatement 成員](../../../connect/jdbc/reference/sqlserverstatement-members.md)   
 [SQLServerStatement 類別](../../../connect/jdbc/reference/sqlserverstatement-class.md)   
 [使用適應性緩衝](../../../connect/jdbc/using-adaptive-buffering.md)  
  
  
