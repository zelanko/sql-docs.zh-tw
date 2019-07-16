---
title: CLR 常式的自訂屬性 |Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.reviewer: ''
ms.technology: clr
ms.topic: reference
helpviewer_keywords:
- routines [CLR integration]
- SqlFacet attribute
- SqlTrigger attribute
- SqlProcedure attribute
- custom attributes [CLR integration]
- SqlUserDefinedAggregate attribute
- attributes [CLR integration]
- SqlMethod attribute
- SqlFunction attribute
- common language runtime [SQL Server], attributes
- SqlUserDefinedTypeAttribute attribute
ms.assetid: 95069d22-b05d-4670-b053-15ee2a664e33
author: rothja
ms.author: jroth
ms.openlocfilehash: 1c1105579dc5da82a66fb101e559e1fb96feac1f
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/15/2019
ms.locfileid: "68138634"
---
# <a name="clr-integration-custom-attributes-for-clr-routines"></a>CLR 常式的 CLR 整合自訂屬性
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  列出的屬性可以套用 common language runtime (CLR) 常式、 使用者定義型別，以及在中註冊的使用者定義彙總[!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]。 如果沒有套用屬性，[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 會假設預設值。 列出的屬性中定義**Microsoft.SqlServer.Server**命名空間。  
  
## <a name="the-sqluserdefinedaggregate-attribute"></a>SqlUserDefinedAggregate 屬性  
 **SqlUserDefinedAggregate**屬性會指出，應該將方法註冊為使用者定義彙總。 每個使用者定義彙總都必須使用這個屬性加註。  
  
 如需詳細資訊，請參閱 < [SqlUserDefinedAggregateAttribute](https://go.microsoft.com/fwlink/?LinkId=124626)。  
  
## <a name="the-sqlfunction-attribute"></a>SqlFunction 屬性  
 **SqlFunction**屬性會指出此方法應該註冊為函式，以適當的函式的屬性集合。  
  
 如需詳細資訊，請參閱 < [SqlFunctionAttribute](https://go.microsoft.com/fwlink/?LinkId=128019)。  
  
## <a name="the-sqlfacet-attribute"></a>SqlFacet 屬性  
 **SqlFacet**屬性用來傳回使用者定義型別 (UDT) 運算式的傳回類型的相關資訊。  
  
 如需詳細資訊，請參閱 < [SqlFacetAttribute](https://go.microsoft.com/fwlink/?LinkId=128020)。  
  
## <a name="the-sqlprocedure-attribute"></a>SqlProcedure 屬性  
 **SqlProcedure**屬性會指出此方法應該註冊為預存程序。 這個屬性只由 Visual Studio 用於自動將指定的方法註冊為預存程序；[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 不會使用該屬性。  
  
 如需詳細資訊，請參閱 < [SqlProcedureAttribute](https://go.microsoft.com/fwlink/?LinkId=128021)。  
  
## <a name="the-sqltrigger-attribute"></a>SqlTrigger 屬性  
 **SqlTrigger**屬性會指出此方法應該註冊為觸發程序。  
  
 如需詳細資訊，請參閱 < [SqlTriggerContext](https://go.microsoft.com/fwlink/?LinkId=128022)並[SqlTriggerAttribute](https://go.microsoft.com/fwlink/?LinkId=203898)。  
  
## <a name="the-sqluserdefinedtypeattribute"></a>SqlUserDefinedTypeAttribute  
 您可以將 SqlUserDefinedTypeAttribute 套用到組件中的類別定義。 它會使 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 建立繫結至包含此自訂屬性之類別定義的使用者定義型別。  
  
 如需詳細資訊，請參閱 < [SqlUserDefinedTypeAttribute](https://go.microsoft.com/fwlink/?LinkId=128024)。  
  
## <a name="the-sqlmethod-attribute"></a>SqlMethod 屬性  
 **SqlMethod**屬性用來表示 udt 的屬性或方法的決定機制和資料存取屬性。  
  
 如需詳細資訊，請參閱 < [SqlMethodAttribute](https://go.microsoft.com/fwlink/?LinkId=128025)。  
  
## <a name="see-also"></a>另請參閱  
 [CLR 使用者定義彙總](../../../relational-databases/clr-integration-database-objects-user-defined-functions/clr-user-defined-aggregates.md)   
 [CLR 使用者定義函式](../../../relational-databases/clr-integration-database-objects-user-defined-functions/clr-user-defined-functions.md)   
 [CLR 使用者定義型別](../../../relational-databases/clr-integration-database-objects-user-defined-types/clr-user-defined-types.md)   
 [CLR 預存程序](https://msdn.microsoft.com/library/bbdd51b2-a9b4-4916-ba6f-7957ac6c3f33)   
 [CLR 觸發程序](https://msdn.microsoft.com/library/302a4e4a-3172-42b6-9cc0-4a971ab49c1c)  
  
  
