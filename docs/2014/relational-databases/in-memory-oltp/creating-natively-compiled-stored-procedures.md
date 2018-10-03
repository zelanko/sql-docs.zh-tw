---
title: 建立原生編譯的預存程序 | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: in-memory-oltp
ms.topic: conceptual
ms.assetid: e6b34010-cf62-4f65-bbdf-117f291cde7b
author: CarlRabeler
ms.author: carlrab
manager: craigg
ms.openlocfilehash: 72c72dc551aa31dc22def397fb38fe09793478ef
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/02/2018
ms.locfileid: "48084508"
---
# <a name="creating-natively-compiled-stored-procedures"></a>建立原生編譯的預存程序
  原生編譯預存程序不會實作完整 [!INCLUDE[tsql](../../includes/tsql-md.md)] 可程式性和查詢介面區。 某些 [!INCLUDE[tsql](../../includes/tsql-md.md)] 建構無法在原生編譯的預存程序內使用。 如需詳細資訊，請參閱 <<c0> [ 原生編譯預存程序中支援的建構](..\in-memory-oltp\supported-features-for-natively-compiled-t-sql-modules.md)。  
  
 但有幾個 [!INCLUDE[tsql](../../includes/tsql-md.md)] 功能只可供原生編譯的預存程序使用：  
  
-   不可部分完成的區塊。 如需詳細資訊，請參閱 [Atomic Blocks](atomic-blocks-in-native-procedures.md)。  
  
-   原生編譯的預存程序中，變數和參數的 `NOT NULL` 條件約束。 您不能指派 `NULL` 值給宣告為 `NOT NULL` 的參數或變數。 如需詳細資訊，請參閱 [DECLARE @local_variable &#40;Transact-SQL&#41;](/sql/t-sql/language-elements/declare-local-variable-transact-sql)。  
  
-   原生編譯預存程序的結構描述繫結。  
  
 使用 [CREATE PROCEDURE &#40;Transact-SQL&#41;](/sql/t-sql/statements/create-procedure-transact-sql)建立原生編譯的預存程序。 下列範例會顯示記憶體最佳化的資料表以及用來將資料列插入資料表中的原生編譯預存程序。  
  
```tsql  
create table dbo.Ord  
(OrdNo integer not null primary key nonclustered,   
 OrdDate datetime not null,   
 CustCode nvarchar(5) not null)   
 with (memory_optimized=on)  
go  
  
create procedure dbo.OrderInsert(@OrdNo integer, @CustCode nvarchar(5))  
with native_compilation, schemabinding, execute as owner  
as   
begin atomic with  
(transaction isolation level = snapshot,  
language = N'English')  
  
  declare @OrdDate datetime = getdate();  
  insert into dbo.Ord (OrdNo, CustCode, OrdDate) values (@OrdNo, @CustCode, @OrdDate);  
end  
go  
```  
  
 在程式碼範例中，`NATIVE_COMPILATION`表示這個[!INCLUDE[tsql](../../includes/tsql-md.md)]預存程序是原生編譯的預存程序。 以下是必要的選項：  
  
|選項|描述|  
|------------|-----------------|  
|`SCHEMABINDING`|原生編譯的預存程序必須繫結至其所參考之物件的結構描述。 這表示，此程序所參考的資料表將無法卸除。 程序中參考的資料表必須包含其結構描述名稱和萬用字元 (\*) 查詢中不允許。 `SCHEMABINDING` 僅適用於原生編譯的預存程序，在這個版本的[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]。|  
|`EXECUTE AS`|原生編譯的預存程序不支援 `EXECUTE AS CALLER` (預設執行內容)。 因此，需要指定執行內容。 選項`EXECUTE AS OWNER`， `EXECUTE AS`*使用者*，和`EXECUTE AS SELF`支援。|  
|`BEGIN ATOMIC`|原生編譯的預存程序主體必須剛好由一個不可部分完成的區塊所組成。 不可部分完成的區塊保證會以不可部分完成的方式執行預存程序。 如果此程序在使用中交易的內容之外叫用，它將會開始新的交易，該交易會在不可部分完成的區塊結尾認可。 原生編譯預存程序中不可部分完成的區塊有兩個必要選項：<br /><br /> `TRANSACTION ISOLATION LEVEL`. 請參閱[交易隔離等級](../../database-engine/transaction-isolation-levels.md)針對支援的隔離等級。<br /><br /> `LANGUAGE`. 預存程序的語言必須設定為其中一個可用語言或語言別名。|  
  
 `EXECUTE AS` 和 Windows 登入可能會因為透過 `EXECUTE AS`執行模擬而發生錯誤。 如果使用者帳戶使用 Windows 驗證，[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 執行個體所使用的服務帳戶與 Windows 登入的網域之間必須完全信任。 否則，在建立原生編譯之預存程序時，即會傳回下列錯誤訊息︰「訊息 15404，無法獲得關於 Windows NT 群組/使用者「使用者名稱」的資訊，錯誤碼 0x5。  
  
 如果要解決此錯誤，請使用下列動作之一：  
  
-   使用與 Windows 使用者位於相同網域的帳戶來執行 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 服務。  
  
-   如果 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 使用電腦帳戶 (例如「網路服務」或「本機系統」)，則包含 Windows 使用者的網域必須信任該電腦。  
  
-   使用 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 驗證。  
  
 建立原生編譯預存程序時，您可能也會看到錯誤 15517。 如需詳細資訊，請參閱 < [MSSQLSERVER_15517](../errors-events/mssqlserver-15517-database-engine-error.md)。  
  
## <a name="updating-a-natively-compiled-stored-procedure"></a>更新原生編譯預存程序  
 不支援對原生編譯的預存程序執行變更作業。 修改原生編譯預存程序的方法之一，是先卸除再重新建立預存程序︰  
  
1.  在預存程序上產生權限的指令碼。  
  
2.  選擇性地產生預存程序的指令碼並儲存為備份。  
  
3.  卸除預存程序。  
  
4.  建立修改的預存程序。  
  
5.  將指令碼撰寫的權限重新套用至預存程序。  
  
 此程序的缺點在於，應用程式將在步驟 3 開始到步驟 5 完成之間離線。 這段時間約為幾秒，且使用應用程式的用戶端可能會看見錯誤訊息。  
  
 (有效) 修改原生編譯預存程序的另一種方式是先建立新版的預存程序。 在這裡，原生編譯的預存程序擁有相關聯的版本號碼。 我們會將舊版稱為 SP_Vold，新版稱為 SP_Vnew。  
  
1.  在 SP_Vold 上產生權限的指令碼。  
  
2.  建立 SP_Vnew。  
  
3.  將 SP_Vold 的權限套用至 SP_Vnew。  
  
4.  更新 SP_Vold 的參考以指向 SP_Vnew。 這項操作可透過不同的方式完成，例如：  
  
     使用包裝函式 (以磁碟為基礎) 預存程序，並將該程序修改為指向 SP_Vnew。 這個方法的缺點是間接造成的效能影響。  
  
    ```tsql  
    ALTER PROCEDURE dbo.SP p1,...,pn  
    AS  
      EXEC dbo.SP_Vnew p1,...,pn  
    GO  
    ```  
  
5.  選擇性地卸除 SP_Vold。  
  
 這個方法的優點是應用程式不會離線。 不過，需要執行更多工作來維護參考，並確認參考一律指向最新版的預存程序。  
  
## <a name="see-also"></a>另請參閱  
 [原生編譯的預存程序](natively-compiled-stored-procedures.md)  
  
  
