# Team Enums

## Location

`InvitationDecision` in `src/enums/InvitationDecision.ts` has `accept` and `decline` values for the invitation response contract. `InvitationStatus` in `src/enums/InvitationStatus.ts` stores `pending`, `accepted`, or `declined` on an invitation. The client shows team-specific leader/member badges based on creator and accepted membership; those are not global user roles.

## Shared Enums Used

| Enum | Location | Usage |
|------|----------|-------|
| `UserRole` | `src/enums/user/UserRole.ts` | Restrict team creation to Admin or Leader; existing creator owns later writes |
