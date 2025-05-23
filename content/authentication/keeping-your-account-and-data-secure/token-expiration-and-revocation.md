---
title: Token expiration and revocation
intro: 'Your tokens can expire and can also be revoked by you, applications you have authorized, and {% data variables.product.github %} itself.'
versions:
  fpt: '*'
  ghes: '*'
  ghec: '*'
topics:
  - Identity
  - Access management
shortTitle: Token expiration
redirect_from:
  - /github/authenticating-to-github/keeping-your-account-and-data-secure/token-expiration-and-revocation
---

When a token has expired or has been revoked, it can no longer be used to authenticate Git and API requests. It is not possible to restore an expired or revoked token, you or the application will need to create a new token.

This article explains the possible reasons your {% data variables.product.github %} token might be revoked or expire.

> [!NOTE]
> When a {% data variables.product.pat_generic %} or OAuth token expires or is revoked, you may see an `oauth_authorization.destroy` action in your security log. For more information, see [AUTOTITLE](/authentication/keeping-your-account-and-data-secure/reviewing-your-security-log).

## Token revoked after reaching its expiration date

When you create a {% data variables.product.pat_generic %}, we recommend that you set an expiration for your token. Upon reaching your token's expiration date, the token is automatically revoked. For more information, see [AUTOTITLE](/authentication/keeping-your-account-and-data-secure/creating-a-personal-access-token).

{% ifversion fpt or ghec %}

## Token revoked when pushed to a public repository or public gist

If a valid OAuth token, {% data variables.product.prodname_github_app %} token, or {% data variables.product.pat_generic %} is pushed to a public repository or public gist, the token will be automatically revoked.

{% endif %}

{% ifversion fpt or ghec %}

## Token expired due to lack of use

{% data variables.product.github %} will automatically revoke an OAuth token or {% data variables.product.pat_generic %} when the token hasn't been used in one year.
{% endif %}

## Token revoked by the user

You can revoke your authorization of a {% data variables.product.prodname_github_app %} or {% data variables.product.prodname_oauth_app %} from your account settings which will revoke any tokens associated with the app. For more information, see [AUTOTITLE](/apps/using-github-apps/reviewing-your-authorized-integrations) and [AUTOTITLE](/apps/oauth-apps/using-oauth-apps/reviewing-your-authorized-applications-oauth).

Once an authorization is revoked, any tokens associated with the authorization will be revoked as well. To reauthorize an application, follow the instructions from the third-party application or website to connect your account on {% data variables.product.prodname_dotcom %} again.

{% ifversion fpt or ghec %}

## Token revoked by a third party

To prevent unauthorized access using exposed tokens, {% data variables.product.github %} recommends token revocation to ensure that a token can no longer be used to authenticate to {% data variables.product.github %}. If you find another user's {% data variables.product.pat_generic %} leaked on {% data variables.product.github %} or elsewhere, you can submit a revocation request through the REST API. See [AUTOTITLE](/rest/credentials/revoke#revoke-a-list-of-credentials).

If a valid {% data variables.product.pat_generic %} is submitted to {% data variables.product.github %}'s credential revocation API, the token will be automatically revoked. This API allows a third party to revoke a token they do not own and helps protect the data associated with this token from unauthorized access, limiting the impact of exposed tokens.

To encourage reports and ensure that exposed tokens can be quickly and easily revoked, we do not require authentication for the revocation requests submitted through the API. As a result, {% data variables.product.github %} is unable to provide further information about the source of the reported token.

{% endif %}

## Token revoked by the {% data variables.product.prodname_oauth_app %}

The owner of an {% data variables.product.prodname_oauth_app %} can revoke an account's authorization of their app, this will also revoke any tokens associated with the authorization. For more information about revoking authorizations of your {% data variables.product.prodname_oauth_app %}, see [AUTOTITLE](/rest/apps/oauth-applications#delete-an-app-authorization).

{% data variables.product.prodname_oauth_app %} owners can also revoke individual tokens associated with an authorization. For more information about revoking individual tokens for your {% data variables.product.prodname_oauth_app %}, see [AUTOTITLE](/rest/apps/oauth-applications#delete-an-app-token).

## Token revoked due to excess of tokens for an {% data variables.product.prodname_oauth_app %} with the same scope

{% data reusables.apps.oauth-token-limit %}

## User token expired due to {% data variables.product.prodname_github_app %} configuration

User access tokens created by a {% data variables.product.prodname_github_app %} will expire after eight hours by default, and then must be regenerated using the included refresh token. Owners of {% data variables.product.prodname_github_apps %} can optionally configure these tokens to never expire instead, but this is not recommended due to the security implications. For more information about configuring your {% data variables.product.prodname_github_app %}'s user access tokens, see [AUTOTITLE](/apps/maintaining-github-apps/activating-optional-features-for-github-apps).
