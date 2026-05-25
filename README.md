<!-- Profile Header (Name and Titles) -->
<div style="margin-top: 80px; text-align: left; padding: 0 40px;">
  <h1 style="font-size: 24px; margin-bottom: 5px;">
    N8N Workflow Automation Projects 
    <!-- Badge Icons (Only Icons, No Names) -->
    <a href="https://github.com/jothirmoysarker">
      <img src="https://img.shields.io/static/v1?label=&message=GitHub&color=181717&logo=github&logoColor=white" alt="GitHub Icon" style="vertical-align: middle; margin-left: 5px;">
    </a>
  </h1>
</div>

# Content Creation Uning Gemini Veo3
<img src="Content Creation Uning Gemini Veo3/Content Creation Uning Gemini Veo3.png" alt="story based" width="800">
<p style="font-size: 16px; color: gray;">This is an n8n workflow built to automatically generate product marketing and ad videos using Gemini Veo3 and publish them to Instagram and TikTok. As of today, n8n's native Gemini video node does not support image input, this workflow solves that by using a custom HTTP Request node to send images directly to Veo3, enabling true image-to-video generation for product ads.</p>
</div>

### Full Flow Summary
```
Schedule Trigger
    → Read Google Sheets
        → Content ready? ──YES──→ Get Today's Style
                                      → Claude generates product ad prompt
                                      → Fetch product image → Convert to Base64
                                      → Add image to prompt
                                      → Slack notification
                                            ↓
                              Custom HTTP Request → Gemini Veo3
                              (image + prompt sent as Base64)
                                            ↓
                                   Wait → Poll → Video ready?
                                      NO  → loop back
                                      YES → Fetch video binary
                                            ↓
                                   Upload to Blotato
                                   ↙              ↘
                            Instagram post      TikTok post
                                   ↓                ↓
                            Slack confirm      Slack confirm
```

# Content Creation (Ad based)
<img src="Content Creation (Ad based)/Instagram And TikTok (Ad).png" alt="Ad based" width="800">
<p style="font-size: 16px; color: gray;">This is an n8n workflow built to automatically generate and publish ad videos to Instagram and TikTok on a schedule. It uses Google Sheets as a control panel, Claude/AI for prompt generation, Gemini Veo3 for video generation, and Blotato for social media publishing.</p>
</div>

### Full Flow Summary

```
Schedule Trigger
    → Read Google Sheets
        → Custom prompt? ──YES──→ Clean → Base64 Image → Gemini Veo3
        → No prompt?    ──NO───→ Claude generates prompt → Base64 Image → Gemini Veo3
                                          ↓
                              Wait → Poll → Get Video Binary
                                          ↓
                          Instagram Upload    TikTok Upload
                                          ↓
                              Update Google Sheet row ✓
```
# Content Creation (story based) + Video Merging
<img src="Content Creation (story based) + Video Merging/Youtube Story.png" alt="story based" width="800">
<p style="font-size: 16px; color: gray;">This is an n8n workflow built to automatically generate long-form AI videos for YouTube Stories by solving Gemini Veo3's 8-second video duration limit. It uses Google Sheets as a script control panel, generates up to 5 separate 8-second clips in parallel using Gemini Veo3, merges them using FFmpeg Micro, and publishes the final video to YouTube.</p>
</div>

### Full Flow Summary
```
Schedule Trigger
    → Read Google Sheets (up to 5 script columns)
        → Claude generates Veo3 prompts
              ↓
    ┌─── Part 1 (Script 1) → Gemini Veo3 → 8s clip ───┐
    ├─── Part 2 (Script 2) → Gemini Veo3 → 8s clip ───┤
    ├─── Part 3 (Script 3) → Gemini Veo3 → 8s clip ───┤  → FFmpeg Micro Merge
    ├─── Part 4 (Script 4) → Gemini Veo3 → 8s clip ───┤     (Upload + Transcode
    └─── Part 5 (Script 5) → Gemini Veo3 → 8s clip ───┘      Subworkflows)
                                                ↓
                                     Final merged video
                                                ↓
                                    Upload to YouTube (Blotato)
                                                ↓
                                   Update Google Sheet row ✓
```

# Content Creation Uning Kie Ai
<img src="Content Creation Uning Kie Ai/Content Creation Uning Kie Ai.png" width="800">
<p style="font-size: 16px; color: gray;">This is an n8n workflow built to automatically generate and publish product ad videos to Instagram and TikTok using Kie AI for video generation. Unlike Gemini Veo3, Kie AI uses a simpler two-HTTP-node pattern: one to submit the video generation request and a second to poll for completion, making the pipeline cleaner while still delivering AI-generated video content.</p>
</div>

### Full Flow Summary
```
Schedule Trigger
    → Read Google Sheets
        → Content ready? ──YES──→ Claude generates product ad prompt
                                      → Format prompt → Add product image
                                      → Slack notification
                                            ↓
                              HTTP Node 1 → POST to Kie AI (submit job)
                                            ↓
                                   Slack: job submitted
                                            ↓
                                         Wait
                                            ↓
                              HTTP Node 2 → GET Kie AI (check status)
                                            ↓
                                       Switch
                              ┌────────────┼────────────┐
                           Success    Generating      Failed
                              ↓           ↓              ↓
                         Continue    loop back      Slack alert
                              ↓
                        Edit Fields → Upload media (Blotato)
                           ↙                      ↘
                    Instagram post             TikTok post
                        ↓                          ↓
                  Slack confirm              Slack confirm
```
