# OneSource Platform

## Introduction

OneSource is an AI-powered multi-platform content creation tool designed for India's 100M+ content creators. The platform transforms a single video into platform-optimized content (video with captions + text posts) for Instagram, LinkedIn, Twitter/X, and Facebook. It features a template-driven approach where users create customizable templates once, then every video upload automatically generates content following their rules. The platform is mobile-first, bilingual (Hindi/English/Hinglish), and addresses the core problem of content creators spending 15+ hours weekly manually repurposing video content across different social media platforms.

## Glossary

- **OneSource_Platform**: The complete AI-powered content creation system
- **Template_System**: The no-code customization engine for content generation rules
- **Video_Processor**: The component handling video upload, storage, and optimization
- **Caption_Generator**: The AI-powered system that creates and burns captions onto videos
- **Content_Generator**: The AI system using Amazon Bedrock to create platform-specific text posts
- **Template_Processor_Agent**: Agent that reads templates, parses rules, and extracts preferences
- **Video_Intelligence_Agent**: Agent that transcribes audio, detects scenes, and processes video
- **Content_Generator_Agent**: Agent that generates platform-specific posts using Amazon Bedrock
- **Preview_Compositor_Agent**: Agent that generates mobile-responsive previews and downloadable packages
- **Brand_Assets**: User-uploaded logos, colors, and taglines for consistent branding
- **Platform_Content**: The combination of optimized video and text post for a specific social media platform
- **Hinglish**: Mixed Hindi-English language commonly used in Indian social media
- **Caption_Burning**: The process of permanently embedding text captions onto video frames

## Requirements

### Requirement 1: Video Upload and Storage

**User Story:** As a content creator, I want to upload videos from my mobile device or computer, so that I can quickly start the content generation process without technical barriers.

#### Acceptance Criteria

1. WHEN a user uploads a video file, THE Video_Processor SHALL accept MP4, MOV, AVI, and WebM formats
2. WHEN a video file exceeds 500MB, THE Video_Processor SHALL reject the upload and display a clear error message
3. WHEN a video duration is less than 15 seconds or greater than 10 minutes, THE Video_Processor SHALL reject the upload and display a duration error message
4. WHEN a valid video is uploaded, THE Video_Processor SHALL store the file in Amazon S3 within 30 seconds for files under 100MB
5. WHEN a user accesses the upload interface from a mobile browser, THE Video_Processor SHALL provide a mobile-optimized upload experience with touch-friendly controls
6. WHEN a video upload is in progress, THE Video_Processor SHALL display real-time upload progress percentage
7. WHEN a video upload fails, THE Video_Processor SHALL allow the user to retry without re-selecting the file

### Requirement 2: Template Creation and Management

**User Story:** As a content creator, I want to create and save customizable templates with my content preferences, so that I don't have to configure settings for every video upload.

#### Acceptance Criteria

1. WHEN a new user first accesses the platform, THE Template_System SHALL provide a default template with pre-configured settings
2. WHEN a user creates a new template, THE Template_System SHALL allow naming the template with up to 50 characters
3. WHEN a user selects a pre-built template option, THE Template_System SHALL offer at least 4 options: "Tech Influencer", "Business Coach", "Fitness Creator", and "Educational Content"
4. WHEN a user customizes template settings, THE Template_System SHALL save brand voice, language preference, platform-specific preferences, hashtag collections, and brand assets
5. WHEN a user saves a template, THE Template_System SHALL persist the template to Amazon DynamoDB within 5 seconds
6. WHEN a user loads a saved template, THE Template_System SHALL retrieve all template settings and apply them to the current session
7. WHEN a user edits an existing template, THE Template_System SHALL update the template without affecting previously generated content
8. WHEN a user has multiple templates, THE Template_System SHALL allow selecting any template as the default for new uploads
9. THE Template_System SHALL support unlimited custom templates per user account

### Requirement 3: Platform-Specific Content Preferences

**User Story:** As a content creator, I want to configure different content styles for each social media platform within my template, so that my content is optimized for each platform's unique audience and format requirements.

#### Acceptance Criteria

1. WHEN a user configures Instagram preferences, THE Template_System SHALL allow setting emoji usage level, hashtag count (5-30), CTA text, caption length preference, first comment hashtag option, and hook style
2. WHEN a user configures LinkedIn preferences, THE Template_System SHALL allow selecting format (short/long/article), tone (professional/casual/thought-leader), professional insights toggle, carousel suggestions toggle, and document formatting option
3. WHEN a user configures Twitter/X preferences, THE Template_System SHALL allow selecting format (single tweet/thread), engagement questions toggle, abbreviations usage, poll suggestions toggle, and character limit awareness
4. WHEN a user configures Facebook preferences, THE Template_System SHALL allow setting community tone, length preference, conversation starters toggle, and group-friendly formatting option
5. WHEN a user saves platform preferences, THE Template_System SHALL validate that all required fields are completed before saving
6. WHEN platform preferences conflict with platform limitations, THE Template_System SHALL display a warning and suggest corrections

### Requirement 4: Bilingual Content Support

**User Story:** As an Indian content creator, I want to generate content in Hindi, English, or Hinglish, so that I can reach my audience in their preferred language and maintain cultural authenticity.

#### Acceptance Criteria

1. WHEN a video contains Hindi audio, THE Video_Intelligence_Agent SHALL transcribe it using Amazon Transcribe with Hindi language model
2. WHEN a video contains English audio, THE Video_Intelligence_Agent SHALL transcribe it using Amazon Transcribe with English language model
3. WHEN a video contains mixed Hindi-English audio, THE Video_Intelligence_Agent SHALL transcribe it using Amazon Transcribe with appropriate language detection
4. WHEN a user selects "English only" output, THE Content_Generator_Agent SHALL generate all text content in English
5. WHEN a user selects "Hindi only" output, THE Content_Generator_Agent SHALL generate all text content in Devanagari script
6. WHEN a user selects "Hinglish" output, THE Content_Generator_Agent SHALL generate text content mixing Hindi and English words naturally
7. WHEN generating Hinglish content, THE Content_Generator_Agent SHALL use culturally appropriate Indian English phrases and expressions
8. WHEN transcription is complete, THE Video_Intelligence_Agent SHALL provide transcription accuracy confidence score above 85%

### Requirement 5: Smart Caption Generation and Burning

**User Story:** As a content creator, I want AI-powered captions automatically added to my videos with customizable styling, so that my content is accessible and engaging across platforms where videos often play without sound.

#### Acceptance Criteria

1. WHEN a video is processed, THE Caption_Generator SHALL create captions synchronized to speech timing with accuracy within 100ms
2. WHEN a user selects a caption style, THE Caption_Generator SHALL offer at least 4 options: bottom-centered, top-centered, creative floating, and word-by-word animation
3. WHEN a user customizes caption appearance, THE Caption_Generator SHALL allow setting font family, size (12-72px), color (RGB/HEX), background color with opacity, and text effects (bold/italic/shadow)
4. WHEN captions are generated, THE Caption_Generator SHALL automatically highlight key moments with different styling based on audio emphasis
5. WHEN a user manually edits caption timing, THE Caption_Generator SHALL provide a timeline editor with frame-level precision
6. WHEN captions are burned onto video, THE Caption_Generator SHALL use FFmpeg to permanently embed captions without quality loss
7. WHEN caption language is set, THE Caption_Generator SHALL match the template's selected output language (English/Hindi/Hinglish)
8. WHEN captions are rendered, THE Caption_Generator SHALL ensure text readability with minimum 4.5:1 contrast ratio against video background

### Requirement 6: Intelligent Hashtag Generation

**User Story:** As a content creator, I want AI-generated relevant hashtags for each platform, so that my content reaches the right audience without manual hashtag research.

#### Acceptance Criteria

1. WHEN content is generated for a platform, THE Content_Generator_Agent SHALL create hashtags using Amazon Bedrock based on video content analysis
2. WHEN generating Instagram hashtags, THE Content_Generator_Agent SHALL create between 5-30 hashtags based on template settings
3. WHEN generating LinkedIn hashtags, THE Content_Generator_Agent SHALL create 3-5 professional hashtags
4. WHEN generating Twitter/X hashtags, THE Content_Generator_Agent SHALL create 1-3 concise hashtags
5. WHEN generating Facebook hashtags, THE Content_Generator_Agent SHALL create 3-7 community-focused hashtags
6. WHEN creating hashtag collections, THE Content_Generator_Agent SHALL mix high-volume (100K+ posts), medium-volume (10K-100K posts), and niche-volume (under 10K posts) hashtags
7. WHEN generating hashtags for Indian content, THE Content_Generator_Agent SHALL include India-specific trending hashtags relevant to the content
8. WHEN output language is Hinglish, THE Content_Generator_Agent SHALL create bilingual hashtags mixing Hindi and English
9. WHEN a user saves favorite hashtags, THE Template_System SHALL store hashtag collections and allow reuse across videos
10. THE Content_Generator_Agent SHALL generate hashtags that are contextually relevant to the video transcript and visual content

### Requirement 7: Brand Consistency Management

**User Story:** As a content creator, I want to maintain consistent branding across all generated content, so that my audience recognizes my content and builds brand recall.

#### Acceptance Criteria

1. WHEN a user uploads a brand logo, THE Template_System SHALL accept PNG files with transparency up to 5MB
2. WHEN a user sets brand colors, THE Template_System SHALL allow defining primary, secondary, and accent colors using RGB or HEX values
3. WHEN a user adds a brand tagline, THE Template_System SHALL accept text up to 100 characters
4. WHEN a user selects logo placement, THE Template_System SHALL offer options: video end card (last 3 seconds), watermark (corner overlay), or none
5. WHEN brand colors are set, THE Video_Intelligence_Agent SHALL apply colors to captions, graphics, and end cards
6. WHEN a brand tagline is configured, THE Content_Generator_Agent SHALL automatically include it in generated posts based on template settings
7. WHEN a logo is placed as watermark, THE Video_Intelligence_Agent SHALL position it with 5% opacity and 10% size in the selected corner
8. WHEN a logo is placed as end card, THE Video_Intelligence_Agent SHALL create a 3-second branded outro with logo and tagline

### Requirement 8: Multi-Platform Content Generation

**User Story:** As a content creator, I want simultaneous content generation for Instagram, LinkedIn, Twitter/X, and Facebook, so that I can distribute my video across all platforms with one upload.

#### Acceptance Criteria

1. WHEN a video is processed with a template, THE Content_Generator_Agent SHALL generate content for all 4 platforms: Instagram, LinkedIn, Twitter/X, and Facebook
2. WHEN generating platform content, THE Content_Generator_Agent SHALL create an optimized video with captions, platform-specific text post, relevant hashtags, and optional CTA for each platform
3. WHEN generating content, THE Content_Generator_Agent SHALL use Amazon Bedrock (Claude Sonnet) for intelligent content adaptation
4. WHEN adapting content tone, THE Content_Generator_Agent SHALL maintain consistent core message while adjusting tone per platform (casual for Instagram, professional for LinkedIn, conversational for Twitter/X, community-focused for Facebook)
5. WHEN generating text posts, THE Content_Generator_Agent SHALL respect platform character limits: Instagram (2,200), LinkedIn (3,000), Twitter/X (280 per tweet), Facebook (63,206)
6. WHEN creating video formats, THE Video_Intelligence_Agent SHALL optimize resolution per platform: Instagram (1080x1350 portrait), LinkedIn (1920x1080 landscape), Twitter/X (1280x720 landscape), Facebook (1280x720 landscape)
7. WHEN all platform content is generated, THE OneSource_Platform SHALL complete processing within 90 seconds for videos under 5 minutes
8. WHEN content follows template rules, THE Content_Generator_Agent SHALL apply all platform-specific preferences defined in the template

### Requirement 9: Visual Preview Dashboard

**User Story:** As a content creator, I want to preview all generated content in platform-accurate simulations before downloading, so that I can verify the content looks correct and make edits if needed.

#### Acceptance Criteria

1. WHEN content generation is complete, THE Preview_Compositor_Agent SHALL display a mobile-responsive dashboard showing all 4 platforms
2. WHEN viewing the preview dashboard, THE Preview_Compositor_Agent SHALL render platform-accurate simulations: Instagram feed layout, LinkedIn post layout, Twitter feed layout, and Facebook post layout
3. WHEN a user views a platform preview, THE Preview_Compositor_Agent SHALL display the video player with burned captions and the generated text post with hashtags
4. WHEN a user interacts with the dashboard on mobile, THE Preview_Compositor_Agent SHALL provide touch-friendly controls with minimum 44x44px tap targets
5. WHEN a user toggles dark/light mode, THE Preview_Compositor_Agent SHALL switch the entire dashboard theme within 200ms
6. WHEN previewing videos, THE Preview_Compositor_Agent SHALL show platform-specific formatting including aspect ratios, caption placement, and branding
7. WHEN the dashboard loads, THE Preview_Compositor_Agent SHALL display all previews within 3 seconds on 4G connection
8. WHEN a user scrolls through platform previews, THE Preview_Compositor_Agent SHALL maintain smooth 60fps scrolling performance

### Requirement 10: Content Editing and Download

**User Story:** As a content creator, I want to edit generated text posts and download content in platform-optimized formats, so that I can make final adjustments and easily publish to each platform.

#### Acceptance Criteria

1. WHEN a user clicks edit on any text post, THE Preview_Compositor_Agent SHALL open a simple text editor with real-time character count
2. WHEN a user edits text content, THE Preview_Compositor_Agent SHALL update the preview in real-time without page reload
3. WHEN a user edits caption timing, THE Caption_Generator SHALL provide a timeline editor showing waveform and caption segments
4. WHEN a user edits caption styling, THE Caption_Generator SHALL re-render the video with new caption appearance within 30 seconds
5. WHEN a user selects download for individual platform, THE Preview_Compositor_Agent SHALL create a ZIP file containing optimized video and text file with post content and hashtags
6. WHEN a user selects download all platforms, THE Preview_Compositor_Agent SHALL create an organized folder structure with subfolders for each platform
7. WHEN a user clicks copy to clipboard, THE Preview_Compositor_Agent SHALL copy the text post with hashtags to system clipboard
8. WHEN videos are downloaded, THE Video_Intelligence_Agent SHALL provide platform-optimized formats: Instagram (MP4, H.264, 1080x1350), LinkedIn (MP4, H.264, 1920x1080), Twitter/X (MP4, H.264, 1280x720), Facebook (MP4, H.264, 1280x720)
9. WHEN download is initiated, THE Preview_Compositor_Agent SHALL start download within 2 seconds
10. WHEN editing text, THE Preview_Compositor_Agent SHALL preserve all formatting, line breaks, and emoji

### Requirement 11: User Authentication and Data Persistence

**User Story:** As a content creator, I want to create an account and securely access my templates and generated content, so that I can work across devices and maintain my content history.

#### Acceptance Criteria

1. WHEN a new user signs up, THE OneSource_Platform SHALL use Amazon Cognito for secure user authentication
2. WHEN a user creates an account, THE OneSource_Platform SHALL require email address and password with minimum 8 characters
3. WHEN a user logs in, THE OneSource_Platform SHALL authenticate credentials and create a secure session token
4. WHEN a user's session expires, THE OneSource_Platform SHALL prompt re-authentication without losing unsaved work
5. WHEN a user saves templates, THE OneSource_Platform SHALL store template data in Amazon DynamoDB associated with user ID
6. WHEN a user logs in from a different device, THE OneSource_Platform SHALL retrieve all saved templates and preferences
7. WHEN a user accesses the platform without authentication, THE OneSource_Platform SHALL allow demo mode with one video upload and no template saving
8. THE OneSource_Platform SHALL encrypt all user data at rest and in transit using AWS encryption standards

### Requirement 12: Video Processing and Optimization

**User Story:** As a content creator, I want my videos automatically optimized for each platform's technical requirements, so that I don't need to manually convert or resize videos.

#### Acceptance Criteria

1. WHEN a video is uploaded, THE Video_Intelligence_Agent SHALL use Amazon Rekognition for scene detection and content analysis
2. WHEN processing video, THE Video_Intelligence_Agent SHALL use FFmpeg for format conversion, resolution adjustment, and caption burning
3. WHEN optimizing for Instagram, THE Video_Intelligence_Agent SHALL convert to 1080x1350 portrait orientation with center-crop if needed
4. WHEN optimizing for LinkedIn, THE Video_Intelligence_Agent SHALL convert to 1920x1080 landscape orientation
5. WHEN optimizing for Twitter/X, THE Video_Intelligence_Agent SHALL convert to 1280x720 landscape orientation with maximum 512MB file size
6. WHEN optimizing for Facebook, THE Video_Intelligence_Agent SHALL convert to 1280x720 landscape orientation
7. WHEN video processing is complete, THE Video_Intelligence_Agent SHALL store all optimized versions in Amazon S3 with organized folder structure
8. WHEN videos are stored, THE OneSource_Platform SHALL use Amazon CloudFront CDN for fast delivery with edge caching
9. WHEN video quality is reduced for platform limits, THE Video_Intelligence_Agent SHALL maintain minimum 720p resolution
10. WHEN processing fails, THE Video_Intelligence_Agent SHALL log error details and notify the user with actionable error message

### Requirement 13: Template Processor Agent

**User Story:** As the system, I need a Template Processor Agent to read and parse user templates, so that content generation follows user-defined rules accurately.

#### Acceptance Criteria

1. WHEN a video upload is initiated with a template, THE Template_Processor_Agent SHALL retrieve the template from Amazon DynamoDB within 1 second
2. WHEN parsing template rules, THE Template_Processor_Agent SHALL extract brand voice, language preference, platform-specific preferences, and hashtag collections
3. WHEN loading brand assets, THE Template_Processor_Agent SHALL retrieve logos and color values from S3 storage
4. WHEN template data is incomplete, THE Template_Processor_Agent SHALL use default values and log missing fields
5. WHEN passing data to other agents, THE Template_Processor_Agent SHALL format preferences into structured JSON schema
6. THE Template_Processor_Agent SHALL validate template data integrity before processing

### Requirement 14: Content Generator Agent with AI

**User Story:** As the system, I need a Content Generator Agent using Amazon Bedrock to create platform-specific posts, so that content is intelligently adapted for each platform's audience and format.

#### Acceptance Criteria

1. WHEN generating content, THE Content_Generator_Agent SHALL use Amazon Bedrock API with Claude Sonnet model
2. WHEN creating platform posts, THE Content_Generator_Agent SHALL receive video transcript, template preferences, and platform specifications
3. WHEN adapting tone, THE Content_Generator_Agent SHALL maintain brand voice while adjusting for platform norms
4. WHEN generating hashtags, THE Content_Generator_Agent SHALL analyze video content and create contextually relevant hashtags
5. WHEN output language is specified, THE Content_Generator_Agent SHALL generate content in the selected language (English/Hindi/Hinglish)
6. WHEN creating Hinglish content, THE Content_Generator_Agent SHALL naturally mix Hindi and English with culturally appropriate expressions
7. WHEN API calls fail, THE Content_Generator_Agent SHALL retry up to 3 times with exponential backoff
8. WHEN content is generated, THE Content_Generator_Agent SHALL ensure all platform character limits are respected

### Requirement 15: API and Serverless Architecture

**User Story:** As the system, I need a scalable serverless architecture to handle video processing and content generation, so that the platform can serve multiple users concurrently without performance degradation.

#### Acceptance Criteria

1. WHEN a user uploads a video, THE OneSource_Platform SHALL trigger AWS Lambda functions for orchestration
2. WHEN Lambda functions execute, THE OneSource_Platform SHALL use Amazon API Gateway for REST API endpoints
3. WHEN processing videos, THE OneSource_Platform SHALL scale Lambda functions automatically based on concurrent requests
4. WHEN storing data, THE OneSource_Platform SHALL use Amazon DynamoDB with on-demand capacity scaling
5. WHEN serving videos, THE OneSource_Platform SHALL use Amazon CloudFront for CDN with edge locations in India
6. WHEN API requests are made, THE OneSource_Platform SHALL respond within 200ms for non-processing endpoints
7. WHEN system load increases, THE OneSource_Platform SHALL maintain performance without manual intervention
8. THE OneSource_Platform SHALL implement API rate limiting to prevent abuse: 10 video uploads per hour for free tier users

### Requirement 16: Mobile-First Responsive Design

**User Story:** As an Indian content creator primarily using mobile devices, I want the entire platform to work seamlessly on my phone browser, so that I can create and manage content without needing a computer.

#### Acceptance Criteria

1. WHEN a user accesses the platform on mobile, THE OneSource_Platform SHALL render a mobile-optimized interface with viewport meta tags
2. WHEN viewing on screens below 768px width, THE OneSource_Platform SHALL stack platform previews vertically for easy scrolling
3. WHEN interacting with controls on mobile, THE OneSource_Platform SHALL provide touch targets minimum 44x44px
4. WHEN uploading from mobile, THE OneSource_Platform SHALL access device camera and gallery through native file picker
5. WHEN editing text on mobile, THE OneSource_Platform SHALL prevent zoom on input focus
6. WHEN loading on 3G/4G networks, THE OneSource_Platform SHALL optimize asset loading with lazy loading and compression
7. WHEN the platform loads on mobile, THE OneSource_Platform SHALL achieve First Contentful Paint within 2 seconds on 4G
8. THE OneSource_Platform SHALL support mobile browsers: Chrome, Safari, Firefox, and Samsung Internet

### Requirement 17: Error Handling and User Feedback

**User Story:** As a content creator, I want clear error messages and processing status updates, so that I understand what's happening and can resolve issues quickly.

#### Acceptance Criteria

1. WHEN video upload fails, THE OneSource_Platform SHALL display specific error message indicating the failure reason (file size, format, duration, network)
2. WHEN video processing is in progress, THE OneSource_Platform SHALL show progress indicators for each stage: upload, transcription, caption generation, content creation
3. WHEN transcription fails, THE Video_Intelligence_Agent SHALL notify user and offer manual transcript upload option
4. WHEN AI content generation fails, THE Content_Generator_Agent SHALL retry automatically and notify user if all retries fail
5. WHEN network connection is lost, THE OneSource_Platform SHALL save progress and allow resume when connection is restored
6. WHEN errors occur, THE OneSource_Platform SHALL log error details to CloudWatch for debugging
7. WHEN processing completes successfully, THE OneSource_Platform SHALL display success notification with preview link
8. THE OneSource_Platform SHALL provide helpful error messages in both English and Hindi based on user language preference

### Requirement 18: Performance and Scalability

**User Story:** As a platform operator, I want the system to handle multiple concurrent users efficiently, so that the platform remains fast and reliable as user base grows.

#### Acceptance Criteria

1. WHEN 100 concurrent users upload videos, THE OneSource_Platform SHALL process all videos without timeout errors
2. WHEN video processing queue grows, THE OneSource_Platform SHALL scale Lambda functions to handle increased load
3. WHEN serving video previews, THE OneSource_Platform SHALL use CloudFront CDN to reduce latency below 100ms for Indian users
4. WHEN database queries are executed, THE OneSource_Platform SHALL use DynamoDB indexes for sub-100ms query response
5. WHEN S3 storage grows, THE OneSource_Platform SHALL implement lifecycle policies to archive old videos after 90 days
6. WHEN API Gateway receives requests, THE OneSource_Platform SHALL handle 1000 requests per second without throttling
7. THE OneSource_Platform SHALL maintain 99.9% uptime for core video processing functionality
8. THE OneSource_Platform SHALL complete end-to-end processing (upload to preview) within 90 seconds for 5-minute videos

### Requirement 19: Cost Optimization and Free Tier

**User Story:** As an individual content creator in India, I want access to a free tier with reasonable limits, so that I can try the platform without financial commitment.

#### Acceptance Criteria

1. WHEN a user signs up for free tier, THE OneSource_Platform SHALL allow 10 video uploads per month
2. WHEN a free tier user uploads a video, THE OneSource_Platform SHALL process it with all features enabled
3. WHEN free tier limits are reached, THE OneSource_Platform SHALL display upgrade prompt with pricing information
4. WHEN storing videos, THE OneSource_Platform SHALL use S3 Intelligent-Tiering to optimize storage costs
5. WHEN Lambda functions execute, THE OneSource_Platform SHALL optimize execution time to minimize compute costs
6. WHEN using Amazon Bedrock, THE OneSource_Platform SHALL batch API calls where possible to reduce per-request costs
7. THE OneSource_Platform SHALL implement automatic cleanup of temporary processing files after 24 hours
8. THE OneSource_Platform SHALL provide usage dashboard showing remaining free tier quota

### Requirement 20: Security and Data Privacy

**User Story:** As a content creator, I want my videos and personal data to be secure and private, so that I can trust the platform with my content.

#### Acceptance Criteria

1. WHEN a user uploads a video, THE OneSource_Platform SHALL encrypt the file in transit using TLS 1.3
2. WHEN videos are stored in S3, THE OneSource_Platform SHALL enable server-side encryption with AWS-managed keys
3. WHEN user data is stored in DynamoDB, THE OneSource_Platform SHALL enable encryption at rest
4. WHEN a user deletes a video, THE OneSource_Platform SHALL permanently remove all associated files from S3 within 24 hours
5. WHEN API requests are made, THE OneSource_Platform SHALL validate authentication tokens on every request
6. WHEN accessing user data, THE OneSource_Platform SHALL implement row-level security ensuring users only access their own data
7. THE OneSource_Platform SHALL comply with data privacy regulations applicable to Indian users
8. THE OneSource_Platform SHALL implement CORS policies to prevent unauthorized cross-origin requests
9. THE OneSource_Platform SHALL sanitize all user inputs to prevent XSS and injection attacks
10. WHEN a user requests data deletion, THE OneSource_Platform SHALL provide complete account and data deletion within 30 days
