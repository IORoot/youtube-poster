# Github Action for posting to YouTube Channel

For setting up Google API OAUTH
See page: https://github.com/porjo/youtubeuploader

## To change youtube channel to post on:

1. Download the client_secret.json
2. use the command line:
```bash
./youtubeuploader -secrets client_secret.json -filename video.mp4
```
3. This will open oAUTH and ask for user details
4. It will then ask you the youtube channel to post on.
5. A new `request.token` file will be generated.
6. Base64 encode for the github action.
```bash
base64 -i request.token -o request.token.b64
base64 -i client_secret.json -o client_secret.b64
```
7. Upload to Github under the Settings > Secrets > Actions as:
    - CLIENT_SECRETS_B64
    - REQUEST_TOKEN_B64


## Example Curl request:

```json
curl -X POST \
  -H "Accept: application/vnd.github+json" \
  -H "Authorization: Bearer github_pat_11111111111111111111111111111111111111111111111111111111111111" \
  https://api.github.com/repos/IORoot/youtube-poster/actions/workflows/update_youtube_v2.yml/dispatches \
  -d '{
    "ref": "master",
    "inputs": {
      "video_url": "https://londonparkour.synology.me:5443/Balance-Mounting/Tutorial-Balancing-Mounting_1-Step-Vault-Reposition.mp4",
      "thumbnail": "https://londonparkour.synology.me:5443/Balance-Mounting/screenshots/Tutorial-Balancing-Mounting_1-Step-Vault-Reposition_1-16_9.png",
      "metadata": "{ \"tags\": null, \"title\": \"Lets Jump, Swing, Vault and Climb! Join Our Epic Parkour Class for Kids.\", \"license\": \"creativeCommon\", \"language\": \"en\", \"publishAt\": \"2024-05-08T04:56:00+00:00\", \"categoryId\": \"10\", \"embeddable\": true, \"description\": \"◣◥ Parkour Kids Classes!\\n\\nLets Jump, Swing, Vault and Climb! Join Our Epic Parkour Class for Kids.\\n\\nAttention all London Kids! Are you ready to take your abilities to the next level? Then come join our parkour class and learn to move like a ninja! \\n\\nOur expert instructor will guide you through the fundamentals of parkour, teaching you how to jump, climb, and vault over obstacles with ease. \\n\\nWith our fun and engaging classes, youll improve your fitness, build confidence, and make new friends along the way. Book now and start your parkour journey today! \\n\\n\\n\\n🟢 Saturdays 9am @Vauxhall. (6-9 age)\\n🟢 Saturdays 10:30am @Vauxhall. (10-14 age)\\n🟢 Sundays 10:30am @Canada Water. (8-14 age)\\n\\n◣◥ LONDONPARKOUR.com\\n\\n#parkour #londonparkour #parkourclass #londonsports  #London #londonsports #kidsparkour #parkour\", \"madeForKids\": false, \"privacyStatus\": \"public\", \"recordingdate\": \"2024-05-08T04:56:00+00:00\", \"publicStatsViewable\": false  }"
    }
  }'
```