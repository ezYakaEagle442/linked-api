# linked-api

Read:
- [https://learn.microsoft.com/en-us/linkedin/marketing/community-management/shares/posts-api?view=li-lms-2025-02&tabs=http#find-posts-by-authors](https://learn.microsoft.com/en-us/linkedin/marketing/community-management/shares/posts-api?view=li-lms-2025-02&tabs=http#find-posts-by-authors)
- [https://learn.microsoft.com/en-us/linkedin/shared/authentication/programmatic-refresh-tokens?context=linkedin%2Fcontext](https://learn.microsoft.com/en-us/linkedin/shared/authentication/programmatic-refresh-tokens?context=linkedin%2Fcontext)
- [https://learn.microsoft.com/en-us/linkedin/shared/authentication/postman-getting-started](https://learn.microsoft.com/en-us/linkedin/shared/authentication/postman-getting-started)
- []()
- []()
- []()
- []()
- []()
- [https://www.linkedin.com/legal/l/api-terms-of-use](https://www.linkedin.com/legal/l/api-terms-of-use):
LinkedIn currently does not charge a fee for use of the APIs, but may choose to in the future.


## pre-req
Go to the [LinkedIn Developer Portal](https://www.linkedin.com/developers/tools/oauth), create a dummy App 'dummy-api-client'. 

Note: For Individual Developers: API products available to individual developers have a default Company page associated with them and you must select that default Company page to proceed.

To learn more about the products and the default Company pages, click [https://www.linkedin.com/help/linkedin/answer/102672](https://www.linkedin.com/help/linkedin/answer/a548360/)

Members in the European Economic Area and Switzerland can build an application to enable continuous and real-time data sharing of their LinkedIn data from LinkedIn to such application through integration with the Member Data Portability API. To gain access to the Member Data Portability API, members must first create a developer application and select a dedicated default Page in order to request access to the Member Data Portability API. 

### Create a LinkedIn page

Read [https://learn.microsoft.com/en-us/linkedin/dma/member-data-portability/member-data-portability-member/?view=li-dma-data-portability-2025-02](https://learn.microsoft.com/en-us/linkedin/dma/member-data-portability/member-data-portability-member/?view=li-dma-data-portability-2025-02)

Create a fake dummy App 'my-company' which URL is provided by LinkedIn: [https://www.linkedin.com/company/member-data-portability-member-default-company/](https://www.linkedin.com/company/member-data-portability-member-default-company/)

Cick on the Auth Tab , get and note in a PRIVATE SECURE storage your ClienID and Primary Client Secret.

Optionnaly:
Create a page for your organization if it does not already exist:
[https://www.linkedin.com/company/setup/new/](https://www.linkedin.com/company/setup/new/)

Go your App page https://www.linkedin.com/developers/apps/XXXXXXXX/auth and cick on the Auth Tab , get and note in a PRIVATE SECURE storage your ClienID and Primary Client Secret.


    get an PAI Token

    [https://www.linkedin.com/oauth/v2/accessToken](https://www.linkedin.com/oauth/v2/accessToken)
    [https://learn.microsoft.com/en-us/linkedin/shared/authentication/client-credentials-flow?context=linkedin%2Fcontext&tabs=cURL1#sample-request-secure-approach](https://learn.microsoft.com/en-us/linkedin/shared/authentication/client-credentials-flow?context=linkedin%2Fcontext&tabs=cURL1#sample-request-secure-approach)

```bash
CLIENT_ID="XXX" # replace with your values
CLIENT_SECRET="XXX" # replace with your values
```

1. Once your application has been successfully provisioned with “Member Data Portability API (Member)” API product, you can generate access tokens via our “OAuth Token Generator Tool”. This can be accessed via the “OAuth Token Tools" under “Docs and tools” drop down menu in the developer portal. 

2. In the OAuth 2.0 Tools, click on "Create token".

3. Select the Application which has been provisioned with the Member Data Portability API (Member) API product. 

4. Select “r_dma_portability_self_serve” as scope and click on “Request access token”. 

5. You will be redirected to login and provide consent to generate the access token. 

6. Once logged in, you would be redirected to consent to share your LinkedIn Data with your application. Please read through the text and if you agree to consent, click "Allow" 

7. he access token has been generated, you can start using this access token to make authenticated API calls to download your LinkedIn data.



```bash
TOKEN="XXX" # replace with your values
```

```console

```

```bash

```

```console

```


```console

```

get the LinkedId ID, the unique identifier of the user:

```bash

# TOKEN=$(curl --location --request POST "https://www.linkedin.com/oauth/v2/accessToken" \
# --header "Content-Type: application/x-www-form-urlencoded" \
# --data-urlencode "grant_type=client_credentials" \
# --data-urlencode "client_id=${CLIENT_ID}" \
# --data-urlencode "client_secret=${CLIENT_SECRET}")

echo "token: " $TOKEN

# curl -H "Authorization: Bearer $TOKEN" \
# "https://api.linkedin.com/v2/me?projection=(id)"
```

```console

```

Find your posts:

- sortBy can be: CREATED (for created time) or LAST_MODIFIED, default is set to LAST_MODIFIED
- count: The number of items you want included on each page of results. There could be fewer items remaining than the value you specify. The default is 10 and maximum allowed count is 100.
- start: The index of the first item you want results for. Default=0

```bash

# curl -X GET "https://api.linkedin.com/rest/posts?author={encoded person urn or organization urn like # urn%3Ali%3Aperson%3A5abc_dEfgH or urn%3Ali%3Aorganization%3A2414183}&q=author&count=10&sortBy=LAST_MODIFIED" \
# -H "X-Restli-Protocol-Version: 2.0.0" \
# -H "LinkedIn-Version: 202502" \
# -H "X-RestLi-Method: FINDER" \
# -H "Authorization: Bearer ${TOKEN}"

# curl -X POST "https://api.linkedin.com/rest/dmaExportJobs" \
#     -H "Authorization: Bearer $TOKEN" \
#     -H "LinkedIn-Version: 202502" \
#     -H "X-RestLi-Protocol-Version: 2.0.0" \
#     -H "Content-Type: application/json" \
#     -d "{}"


# curl -H "Authorization: Bearer $TOKEN" \
#      -H "LinkedIn-Version: 202502" \
#      "https://api.linkedin.com/rest/dmaExportMembership"

# curl -H "Authorization: Bearer $TOKEN" \
#      -H "LinkedIn-Version: 202502" \
#      "https://api.linkedin.com/rest/dmaExportMember"

# curl -X GET "https://api.linkedin.com/rest/memberSnapshotData?q=me" \
#     -H "Authorization: Bearer $TOKEN" \
#     -H "LinkedIn-Version: 202312"

# https://learn.microsoft.com/en-us/linkedin/dma/member-data-portability/shared/snapshot-domain?view=li-dma-data-portability-2025-02#member-snapshot-domain-list

# Liste des domaines
domains=(
  "ADS_CLICKED" "MEMBER_FOLLOWING" "LOGIN" "RICH_MEDIA" "SEARCHES" "INFERENCE_TAKEOUT"
  "ALL_COMMENTS" "CONTACTS" "EVENTS" "RECEIPTS" "AD_TARGETING" "REGISTRATION" "REVIEWS"
  "ARTICLES" "PATENTS" "GROUPS" "COMPANY_FOLLOWS" "INVITATIONS" "PHONE_NUMBERS" "CONNECTIONS"
  "EMAIL_ADDRESSES" "JOB_POSTINGS" "JOB_APPLICATIONS" "JOB_SEEKER_PREFERENCES" "LEARNING"
  "INBOX" "SAVED_JOBS" "SAVED_JOB_ALERTS" "PROFILE" "SKILLS" "POSITIONS" "EDUCATION"
  "TEST_SCORES" "CAUSES_YOU_CARE_ABOUT" "PUBLICATIONS" "PROJECTS" "ORGANIZATIONS" "LANGUAGES"
  "HONORS" "COURSES" "CERTIFICATIONS" "CALENDAR" "RECOMMENDATIONS" "ENDORSEMENTS"
  "MEMBER_SHARE_INFO" "SECURITY_CHALLENGE_PIPE" "TRUSTED_GRAPH" "MARKETPLACE_ENGAGEMENTS"
  "MARKETPLACE_PROVIDERS" "MARKETPLACE_OPPORTUNITIES" "ACTOR_SAVE_ITEM" "JOB_APPLICANT_SAVED_ANSWERS"
  "TALENT_QUESTION_SAVED_RESPONSE" "PROFILE_SUMMARY" "ALL_LIKES" "ALL_VOTES" "RECEIPTS_LBP"
  "LEARNING_COACH_AI_TAKEOUT" "LEARNING_COACH_INBOX" "LEARNING_ROLEPLAY_INBOX" "VOLUNTEERING_EXPERIENCES"
  "ACCOUNT_HISTORY" "INSTANT_REPOSTS"
)


curl --location --request POST "https://api.linkedin.com/rest/memberAuthorizations" \
--header "LinkedIn-Version: 202312" \
--header "Authorization: Bearer $TOKEN" \
--header "Content-Type: application/json" \
--data-raw "{}"

curl --location --request GET "https://api.linkedin.com/rest/memberAuthorizations?q=memberAndApplication" \
--header "LinkedIn-Version: 202312" \
--header "Authorization: Bearer $TOKEN" \
--header "Content-Type: application/json"
```

```console
{"paging":{"start":0,"count":10,"links":[]},
    "elements":[
        {
            "regulatedAt":1234566891011,
            "memberComplianceScopes":[
                "DMA"
            ],
            "memberComplianceAuthorizationKey": {
                "developerApplication":"urn:li:developerApplication:123456",
                "member":"urn:li:person:123ABC"
            }
        }
    ]
}
```

```bash

# Initialisation des variables
count=10
start=0

# Boucle pour chaque domaine
for domain in "${domains[@]}"; do
  echo "Fetching data for domain: $domain"

  # Initialisation de la pagination
  total=0
  max_results=0

  # Boucle pour la pagination
  while true; do
    # Effectuer la requête API pour le domaine
    response=$(curl --location --request GET "https://api.linkedin.com/rest/memberSnapshotData?q=criteria&count=$count&domain=$domain&start=$start" \
    --header "LinkedIn-Version: 202312" \
    --header "Authorization: Bearer $TOKEN" \
    --header "Content-Type: application/json")

    # Sauvegarder la réponse dans un fichier JSON
    echo "$response" > "linked_DigitalMarketsAct_API_${domain}.json"

    # Affiche le nombre total de résultats
    max_results=$(echo "$response" | jq -r '.paging.total')
    echo "Total results available for domain '$domain': $max_results"

    # Vérifie si une page suivante existe
    next_page=$(echo "$response" | jq -r '.paging.links[] | select(.rel == "next") | .href')

    # Si une page suivante existe, on met à jour l'index `start` pour la prochaine requête
    if [[ -z "$next_page" ]]; then
      break  # Si aucune page suivante, on sort de la boucle
    fi

    # Mets à jour le paramètre `start` pour la prochaine page
    start=$(echo "$next_page" | sed 's/.*start=\([0-9]*\).*/\1/')

    # Si on a déjà récupéré tous les résultats, on sort de la boucle
    if [ "$start" -ge "$max_results" ]; then
      break
    fi
  done
done

```

