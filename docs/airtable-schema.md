# Airtable Schema

Base name: `AWFII MVP`

## Chatbot_Logs
| Column | Type |
|---|---|
| SessionID | Single line text |
| PhoneHash | Single line text |
| UserMessage | Long text |
| Timestamp | Date |
| BotResponse | Long text |
| Language | Single line text |
| FlaggedForReview | Checkbox |
| MentorRequested | Checkbox |
| User_Profiles | Linked record |

## Applicants
| Column | Type |
|---|---|
| ApplicantID | Single line text |
| FullName | Single line text |
| Email | Single line text |
| Phone | Phone number |
| ProgrammeApplied | Single line text |
| Goals | Long text |
| Experience | Long text |
| AIDecision | Single select (APPROVED, WAITLIST, NEEDS_REVIEW) |
| Confidence | Number (integer) |
| AIReasoning | Long text |
| FinalDecision | Single select (APPROVED, WAITLIST, NEEDS_REVIEW) |
| StaffNotes | Long text |
| SubmittedAt | Date |
| ProcessedAt | Date |
| ModelVersion | Single line text |
| User_Profiles | Linked record |

## User_Profiles
| Column | Type |
|---|---|
| PhoneHash | Single line text |
| Name | Single line text |
| Country | Single line text |
| Stage | Single line text |
| ProgrammeFit | Single line text |
| Goals | Long text |
| Experience | Long text |
| ConversationHistory | Long text |
| CreatedAt | Date |
| LastSeen | Date |
| Applicant_Link | Linked record |
| Chatbot_Log_Sessions | Linked record |
| User_States | Linked record |
| FAQs | Linked record |
| Conversation_History | Linked record |

## User_States
| Column | Type |
|---|---|
| Phone_Number | Phone number |
| Current_State | Single select (START, CONSENT_PENDING, REGISTERED, HELP, NAME_PENDING) |
| User_Name | Single line text |
| Last_Interaction | Date (formula: `LAST_MODIFIED_TIME()`) |
| User_Profile_Link | Linked record |
| Conversation_History | Linked record |

## FAQs
| Column | Type |
|---|---|
| Question | Long text |
| Answer | Long text |
| Category | Single select (Saving, Budgeting, Credit, General) |
| Related_User_Profiles | Linked record |

## Conversation_History
| Column | Type |
|---|---|
| Message | Long text |
| Phone | Single line text |
| Role | Single select (user, assistant) |
| Timestamp | Date |
| User_State_Link | Linked record |
| User_Profile_Link | Linked record |

