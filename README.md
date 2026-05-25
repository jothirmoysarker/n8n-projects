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

# Content Creation (Ad based)
<img src="Content Creation (Ad based)/Instagram And TikTok (Ad).png" alt="Claude" width="800">
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
<img src="Content Creation (Ad based)/Instagram And TikTok (Ad).png" alt="Claude" width="800">
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
