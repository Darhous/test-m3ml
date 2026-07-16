# Build vs. Buy — SSO / OIDC / OAuth

Same weighted scoring as `../authentication/08-build-vs-buy.md` applies
— this Feature is not independently re-scored since it shares the exact
same candidate set and the same Engine decision. Building a
standards-compliant OIDC/OAuth2 Provider and SAML/OIDC federation broker
from scratch would score even lower than building basic authentication
(higher protocol-conformance risk, and federation bugs are a well-known
source of real-world authentication bypass vulnerabilities industry-wide)
— reinforcing, not weakening, the `authentication` Feature's Buy
conclusion.
