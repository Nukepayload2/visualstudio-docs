---
title: "IDebugMessageEvent2::SetResponse | Microsoft Docs"
ms.custom: ""
ms.date: "2018-06-30"
ms.prod: "visual-studio-dev14"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "vs-ide-sdk"
ms.tgt_pltfrm: ""
ms.topic: "article"
f1_keywords: 
  - "IDebugMessageEvent2::SetResponse"
helpviewer_keywords: 
  - "IDebugMessageEvent2::SetResponse method"
  - "SetResponse method"
ms.assetid: 2a5e318d-3225-4abd-83f1-28323baff6c0
caps.latest.revision: 11
ms.author: "gregvanl"
manager: "ghogen"
---
# IDebugMessageEvent2::SetResponse
[!INCLUDE[vs2017banner](../../../includes/vs2017banner.md)]

The latest version of this topic can be found at [IDebugMessageEvent2::SetResponse](https://docs.microsoft.com/visualstudio/extensibility/debugger/reference/idebugmessageevent2-setresponse).  
  
Sets the response, if any, from the message box.  
  
## Syntax  
  
```cpp#  
HRESULT SetResponse(   
   DWORD dwResponse  
);  
```  
  
```csharp  
int SetResponse(   
   uint dwResponse  
);  
```  
  
#### Parameters  
 `dwResponse`  
 [in] Specifies the response, using the conventions of the Win32 `MessageBox` function. See the [AfxMessageBox](http://msdn.microsoft.com/library/d66d0328-cdcc-48f6-96a4-badf089099c8) function for details.  
  
## Return Value  
 If successful, returns `S_OK`; otherwise, returns an error code.  
  
## See Also  
 [IDebugMessageEvent2](../../../extensibility/debugger/reference/idebugmessageevent2.md)   
 [AfxMessageBox](http://msdn.microsoft.com/library/d66d0328-cdcc-48f6-96a4-badf089099c8)
