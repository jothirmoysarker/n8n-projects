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
