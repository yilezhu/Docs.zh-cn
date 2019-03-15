---
title: 在 ASP.NET Core 中的策略方案
author: rick-anderson
description: 身份验证策略方案，更便于具有单一逻辑身份验证方案
ms.author: riande
ms.date: 2/28/2019
uid: security/authentication/policyschemes
ms.openlocfilehash: c310b61e14df2b7846e32a602bb75914a5850aff
ms.sourcegitcommit: 036d4b03fd86ca5bb378198e29ecf2704257f7b2
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/05/2019
ms.locfileid: "57346717"
---
# <a name="policy-schemes-in-aspnet-core"></a><span data-ttu-id="df587-103">在 ASP.NET Core 中的策略方案</span><span class="sxs-lookup"><span data-stu-id="df587-103">Policy schemes in ASP.NET Core</span></span>

<span data-ttu-id="df587-104">身份验证策略方案更加轻松地有可能使用多个方法的单一逻辑身份验证方案。</span><span class="sxs-lookup"><span data-stu-id="df587-104">Authentication policy schemes make it easier to have a single logical authentication scheme potentially use multiple approaches.</span></span> <span data-ttu-id="df587-105">例如，策略方案可能使用的挑战，Google 身份验证和 cookie 身份验证的其他所有内容。</span><span class="sxs-lookup"><span data-stu-id="df587-105">For example, a policy scheme might use Google authentication for challenges, and cookie authentication for everything else.</span></span> <span data-ttu-id="df587-106">身份验证策略方案使其：</span><span class="sxs-lookup"><span data-stu-id="df587-106">Authentication policy schemes make it:</span></span>

* <span data-ttu-id="df587-107">轻松地将转发到另一个方案的任何身份验证操作。</span><span class="sxs-lookup"><span data-stu-id="df587-107">Easy to forward any authentication action to another scheme.</span></span>
* <span data-ttu-id="df587-108">正向动态根据该请求。</span><span class="sxs-lookup"><span data-stu-id="df587-108">Forward dynamically based on the request.</span></span>

<span data-ttu-id="df587-109">使用派生的所有身份验证方案<xref:Microsoft.AspNetCore.Authentication.AuthenticationSchemeOptions>和关联[ `AuthenticationHandler<TOptions>` ](/dotnet/api/microsoft.aspnetcore.authentication.authenticationhandler-1):</span><span class="sxs-lookup"><span data-stu-id="df587-109">All authentication schemes that use derived <xref:Microsoft.AspNetCore.Authentication.AuthenticationSchemeOptions> and the associated [`AuthenticationHandler<TOptions>`](/dotnet/api/microsoft.aspnetcore.authentication.authenticationhandler-1):</span></span>

* <span data-ttu-id="df587-110">会自动在 ASP.NET Core 2.1 及更高版本的策略方案。</span><span class="sxs-lookup"><span data-stu-id="df587-110">Are automatically policy schemes in ASP.NET Core 2.1 and later.</span></span>
* <span data-ttu-id="df587-111">可以通过配置方案的选项来启用。</span><span class="sxs-lookup"><span data-stu-id="df587-111">Can be enabled via configuring the scheme's options.</span></span>

[!code-csharp[sample](policyschemes/samples/AuthenticationSchemeOptions.cs?name=snippet)]

## <a name="examples"></a><span data-ttu-id="df587-112">示例</span><span class="sxs-lookup"><span data-stu-id="df587-112">Examples</span></span>

<span data-ttu-id="df587-113">下面的示例演示结合了较低级别方案的更高级别方案。</span><span class="sxs-lookup"><span data-stu-id="df587-113">The following example shows a higher level scheme that combines lower level schemes.</span></span> <span data-ttu-id="df587-114">Google 身份验证用于挑战，并为其他所有使用 cookie 身份验证：</span><span class="sxs-lookup"><span data-stu-id="df587-114">Google authentication is used for challenges, and cookie authentication is used for everything else:</span></span>

[!code-csharp[sample](policyschemes/samples/Startup.cs?name=snippet1)]

<span data-ttu-id="df587-115">下面的示例可动态选择基于每个请求的方案。</span><span class="sxs-lookup"><span data-stu-id="df587-115">The following example enables dynamic selection of schemes on a per request basis.</span></span> <span data-ttu-id="df587-116">它是如何混合使用 cookie 和 API 身份验证。</span><span class="sxs-lookup"><span data-stu-id="df587-116">That is, how to mix cookies and API authentication.</span></span>

 <!-- REVIEW, missing If set in public Func<HttpContext, string> ForwardDefaultSelector -->

[!code-csharp[sample](policyschemes/samples/Startup.cs?name=snippet2)]