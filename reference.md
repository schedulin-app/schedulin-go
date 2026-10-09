# Reference
## Posts
<details><summary><code>client.Posts.List() -> *schedulin.ListPostsResponse</code></summary>
<dl>
<dd>

#### 📝 Description

<dl>
<dd>

<dl>
<dd>

Search and filter posts with various criteria including status, date range, social accounts, and tags
</dd>
</dl>
</dd>
</dl>

#### 🔌 Usage

<dl>
<dd>

<dl>
<dd>

```go
request := &schedulin.ListPostsRequest{}
client.Posts.List(
    context.TODO(),
    request,
)
```
</dd>
</dl>
</dd>
</dl>

#### ⚙️ Parameters

<dl>
<dd>

<dl>
<dd>

**page:** `*int` 
    
</dd>
</dl>

<dl>
<dd>

**status:** `*schedulin.ListPostsRequestStatus` 
    
</dd>
</dl>

<dl>
<dd>

**statuses:** `*schedulin.ListPostsRequestStatusesItem` 
    
</dd>
</dl>

<dl>
<dd>

**approvalStatus:** `*schedulin.ListPostsRequestApprovalStatus` 
    
</dd>
</dl>

<dl>
<dd>

**scheduledAt:** `*schedulin.ListPostsRequestScheduledAt` 
    
</dd>
</dl>

<dl>
<dd>

**tagIDs:** `*string` 
    
</dd>
</dl>

<dl>
<dd>

**tagMode:** `*schedulin.ListPostsRequestTagMode` 
    
</dd>
</dl>

<dl>
<dd>

**socialAccountIDs:** `*string` 
    
</dd>
</dl>

<dl>
<dd>

**limit:** `*int` 
    
</dd>
</dl>
</dd>
</dl>


</dd>
</dl>
</details>

<details><summary><code>client.Posts.Create(request) -> *schedulin.CreatePostsResponse</code></summary>
<dl>
<dd>

#### 📝 Description

<dl>
<dd>

<dl>
<dd>

Create a new post with media, tags, and scheduling options. Media items may reference a stored library URL or any publicly reachable image/video URL — external URLs are downloaded into the media library automatically, so clients that cannot issue a raw presigned PUT can attach media in one call.
</dd>
</dl>
</dd>
</dl>

#### 🔌 Usage

<dl>
<dd>

<dl>
<dd>

```go
request := &schedulin.PostCreate{
    Caption: "caption",
    SocialAccountID: "socialAccountId",
}
client.Posts.Create(
    context.TODO(),
    request,
)
```
</dd>
</dl>
</dd>
</dl>

#### ⚙️ Parameters

<dl>
<dd>

<dl>
<dd>

**caption:** `string` 
    
</dd>
</dl>

<dl>
<dd>

**title:** `*string` 
    
</dd>
</dl>

<dl>
<dd>

**scheduledAt:** `*time.Time` 
    
</dd>
</dl>

<dl>
<dd>

**socialAccountID:** `string` 
    
</dd>
</dl>

<dl>
<dd>

**media:** `[]*schedulin.PostCreateMediaItem` 
    
</dd>
</dl>

<dl>
<dd>

**thumbnail:** `*schedulin.PostCreateThumbnail` 
    
</dd>
</dl>

<dl>
<dd>

**platformConfiguration:** `map[string]any` 
    
</dd>
</dl>

<dl>
<dd>

**tagIDs:** `[]string` 
    
</dd>
</dl>

<dl>
<dd>

**action:** `*schedulin.PostCreateAction` 
    
</dd>
</dl>

<dl>
<dd>

**parts:** `[]*schedulin.PostCreatePartsItem` 
    
</dd>
</dl>
</dd>
</dl>


</dd>
</dl>
</details>

<details><summary><code>client.Posts.CountByTab() -> *schedulin.CountByTabPostsResponse</code></summary>
<dl>
<dd>

#### 📝 Description

<dl>
<dd>

<dl>
<dd>

Returns counts of posts for the Queue, Drafts, Approvals, and Sent tabs
</dd>
</dl>
</dd>
</dl>

#### 🔌 Usage

<dl>
<dd>

<dl>
<dd>

```go
request := &schedulin.CountByTabPostsRequest{}
client.Posts.CountByTab(
    context.TODO(),
    request,
)
```
</dd>
</dl>
</dd>
</dl>

#### ⚙️ Parameters

<dl>
<dd>

<dl>
<dd>

**socialAccountIDs:** `*string` 
    
</dd>
</dl>
</dd>
</dl>


</dd>
</dl>
</details>

<details><summary><code>client.Posts.Retrieve(ID) -> *schedulin.PostWithRelations</code></summary>
<dl>
<dd>

#### 📝 Description

<dl>
<dd>

<dl>
<dd>

Retrieve a single post by its ID with all relations
</dd>
</dl>
</dd>
</dl>

#### 🔌 Usage

<dl>
<dd>

<dl>
<dd>

```go
request := &schedulin.RetrievePostsRequest{
    ID: "id",
}
client.Posts.Retrieve(
    context.TODO(),
    request,
)
```
</dd>
</dl>
</dd>
</dl>

#### ⚙️ Parameters

<dl>
<dd>

<dl>
<dd>

**id:** `string` 
    
</dd>
</dl>
</dd>
</dl>


</dd>
</dl>
</details>

<details><summary><code>client.Posts.Update(ID, request) -> *schedulin.Post</code></summary>
<dl>
<dd>

#### 📝 Description

<dl>
<dd>

<dl>
<dd>

Update an existing draft or scheduled post by its ID. `title` sets the post-level title; on Facebook it's an alias for `platformConfiguration.title` (the video title), and either one updates both. Send null or an empty string to clear it. `status` may be DRAFT, SCHEDULED (requires a future `scheduledAt`, either in this request or already on the post), or PROCESSING (publish now). COMPLETED and FAILED are set only by the publisher. A new `scheduledAt` must not be in the past, whatever the status (422). `media` replaces the post's media and accepts the same items as create — a stored or public URL (`{ url }`) or a media library id (`{ id }`), so the `media` array from `GET /v0/posts/{id}` can be sent back as-is. `parts` (X and Mastodon only) replaces the post's thread with the same items create accepts — part media may also be a library `{ id }`, so the `parts` array from `GET /v0/posts/{id}` round-trips — and an empty array removes the thread. On X, parts[0] is the opening tweet: sending `parts` without `caption` sets the caption to parts[0], and changing `caption` or `media` without `parts` updates parts[0] when it matched the old value. Posts that are already publishing, published, or failed can't be edited (409).
</dd>
</dl>
</dd>
</dl>

#### 🔌 Usage

<dl>
<dd>

<dl>
<dd>

```go
request := &schedulin.UpdatePostsRequest{
    ID: "id",
}
client.Posts.Update(
    context.TODO(),
    request,
)
```
</dd>
</dl>
</dd>
</dl>

#### ⚙️ Parameters

<dl>
<dd>

<dl>
<dd>

**id:** `string` 
    
</dd>
</dl>

<dl>
<dd>

**caption:** `*string` 
    
</dd>
</dl>

<dl>
<dd>

**title:** `*string` 
    
</dd>
</dl>

<dl>
<dd>

**scheduledAt:** `*time.Time` 
    
</dd>
</dl>

<dl>
<dd>

**media:** `[]*schedulin.UpdatePostsRequestMediaItem` 
    
</dd>
</dl>

<dl>
<dd>

**platformConfiguration:** `map[string]any` 
    
</dd>
</dl>

<dl>
<dd>

**status:** `*schedulin.UpdatePostsRequestStatus` 
    
</dd>
</dl>

<dl>
<dd>

**tagIDs:** `[]string` 
    
</dd>
</dl>

<dl>
<dd>

**parts:** `[]*schedulin.UpdatePostsRequestPartsItem` 
    
</dd>
</dl>
</dd>
</dl>


</dd>
</dl>
</details>

<details><summary><code>client.Posts.Delete(ID, request) -> *schedulin.Post</code></summary>
<dl>
<dd>

#### 📝 Description

<dl>
<dd>

<dl>
<dd>

Delete a post by its ID
</dd>
</dl>
</dd>
</dl>

#### 🔌 Usage

<dl>
<dd>

<dl>
<dd>

```go
request := &schedulin.DeletePostsRequest{
    ID: "id",
}
client.Posts.Delete(
    context.TODO(),
    request,
)
```
</dd>
</dl>
</dd>
</dl>

#### ⚙️ Parameters

<dl>
<dd>

<dl>
<dd>

**id:** `string` 
    
</dd>
</dl>
</dd>
</dl>


</dd>
</dl>
</details>

<details><summary><code>client.Posts.AnalyticsSummary(ID) -> *schedulin.AnalyticsSummaryPostsResponse</code></summary>
<dl>
<dd>

#### 📝 Description

<dl>
<dd>

<dl>
<dd>

Retrieve the latest analytics snapshot for a post
</dd>
</dl>
</dd>
</dl>

#### 🔌 Usage

<dl>
<dd>

<dl>
<dd>

```go
request := &schedulin.AnalyticsSummaryPostsRequest{
    ID: "id",
}
client.Posts.AnalyticsSummary(
    context.TODO(),
    request,
)
```
</dd>
</dl>
</dd>
</dl>

#### ⚙️ Parameters

<dl>
<dd>

<dl>
<dd>

**id:** `string` 
    
</dd>
</dl>
</dd>
</dl>


</dd>
</dl>
</details>

<details><summary><code>client.Posts.AnalyticsSeries(ID) -> *schedulin.AnalyticsSeriesPostsResponse</code></summary>
<dl>
<dd>

#### 📝 Description

<dl>
<dd>

<dl>
<dd>

Retrieve time series analytics metrics for a post
</dd>
</dl>
</dd>
</dl>

#### 🔌 Usage

<dl>
<dd>

<dl>
<dd>

```go
request := &schedulin.AnalyticsSeriesPostsRequest{
    ID: "id",
}
client.Posts.AnalyticsSeries(
    context.TODO(),
    request,
)
```
</dd>
</dl>
</dd>
</dl>

#### ⚙️ Parameters

<dl>
<dd>

<dl>
<dd>

**id:** `string` 
    
</dd>
</dl>

<dl>
<dd>

**limit:** `*int` 
    
</dd>
</dl>
</dd>
</dl>


</dd>
</dl>
</details>

<details><summary><code>client.Posts.PublishDraft(ID, request) -> *schedulin.Post</code></summary>
<dl>
<dd>

#### 📝 Description

<dl>
<dd>

<dl>
<dd>

Publish a draft post to connected social media accounts
</dd>
</dl>
</dd>
</dl>

#### 🔌 Usage

<dl>
<dd>

<dl>
<dd>

```go
request := &schedulin.PublishDraftPostsRequest{
    ID: "id",
}
client.Posts.PublishDraft(
    context.TODO(),
    request,
)
```
</dd>
</dl>
</dd>
</dl>

#### ⚙️ Parameters

<dl>
<dd>

<dl>
<dd>

**id:** `string` 
    
</dd>
</dl>

<dl>
<dd>

**scheduledAt:** `*time.Time` 
    
</dd>
</dl>
</dd>
</dl>


</dd>
</dl>
</details>

<details><summary><code>client.Posts.UpdateTags(ID, request) -> *schedulin.Post</code></summary>
<dl>
<dd>

#### 📝 Description

<dl>
<dd>

<dl>
<dd>

Replace all tags on a post. No status restrictions apply.
</dd>
</dl>
</dd>
</dl>

#### 🔌 Usage

<dl>
<dd>

<dl>
<dd>

```go
request := &schedulin.UpdateTagsPostsRequest{
    ID: "id",
    TagIDs: []string{
        "tagIds",
    },
}
client.Posts.UpdateTags(
    context.TODO(),
    request,
)
```
</dd>
</dl>
</dd>
</dl>

#### ⚙️ Parameters

<dl>
<dd>

<dl>
<dd>

**id:** `string` 
    
</dd>
</dl>

<dl>
<dd>

**tagIDs:** `[]string` 
    
</dd>
</dl>
</dd>
</dl>


</dd>
</dl>
</details>

## SocialAccounts
<details><summary><code>client.SocialAccounts.List() -> *schedulin.ListSocialAccountsResponse</code></summary>
<dl>
<dd>

#### 📝 Description

<dl>
<dd>

<dl>
<dd>

Retrieve all connected social media accounts for the authenticated user
</dd>
</dl>
</dd>
</dl>

#### 🔌 Usage

<dl>
<dd>

<dl>
<dd>

```go
client.SocialAccounts.List(
    context.TODO(),
)
```
</dd>
</dl>
</dd>
</dl>


</dd>
</dl>
</details>

<details><summary><code>client.SocialAccounts.ListWhopCompanies(ID) -> *schedulin.ListWhopCompaniesSocialAccountsResponse</code></summary>
<dl>
<dd>

#### 📝 Description

<dl>
<dd>

<dl>
<dd>

List companies available to a connected Whop account. Select one before requesting its forum experiences.
</dd>
</dl>
</dd>
</dl>

#### 🔌 Usage

<dl>
<dd>

<dl>
<dd>

```go
request := &schedulin.ListWhopCompaniesSocialAccountsRequest{
    ID: "id",
}
client.SocialAccounts.ListWhopCompanies(
    context.TODO(),
    request,
)
```
</dd>
</dl>
</dd>
</dl>

#### ⚙️ Parameters

<dl>
<dd>

<dl>
<dd>

**id:** `string` 
    
</dd>
</dl>
</dd>
</dl>


</dd>
</dl>
</details>

<details><summary><code>client.SocialAccounts.ListWhopForums(ID) -> *schedulin.ListWhopForumsSocialAccountsResponse</code></summary>
<dl>
<dd>

#### 📝 Description

<dl>
<dd>

<dl>
<dd>

List forum experiences for a Whop company. Use an item id as platformConfiguration.experience.
</dd>
</dl>
</dd>
</dl>

#### 🔌 Usage

<dl>
<dd>

<dl>
<dd>

```go
request := &schedulin.ListWhopForumsSocialAccountsRequest{
    ID: "id",
    CompanyID: "companyId",
}
client.SocialAccounts.ListWhopForums(
    context.TODO(),
    request,
)
```
</dd>
</dl>
</dd>
</dl>

#### ⚙️ Parameters

<dl>
<dd>

<dl>
<dd>

**id:** `string` 
    
</dd>
</dl>

<dl>
<dd>

**companyID:** `string` 
    
</dd>
</dl>
</dd>
</dl>


</dd>
</dl>
</details>

<details><summary><code>client.SocialAccounts.ListDiscordChannels(ID) -> *schedulin.ListDiscordChannelsSocialAccountsResponse</code></summary>
<dl>
<dd>

#### 📝 Description

<dl>
<dd>

<dl>
<dd>

List the text and announcement channels the Schedulin bot can post into for a connected Discord server — only channels where the bot's effective permissions (its roles plus the channel's permission overwrites) include View Channel and Send Messages; channels it can't post in are omitted. Use an item id as `platformConfiguration.channel` when creating a Discord post.
</dd>
</dl>
</dd>
</dl>

#### 🔌 Usage

<dl>
<dd>

<dl>
<dd>

```go
request := &schedulin.ListDiscordChannelsSocialAccountsRequest{
    ID: "id",
}
client.SocialAccounts.ListDiscordChannels(
    context.TODO(),
    request,
)
```
</dd>
</dl>
</dd>
</dl>

#### ⚙️ Parameters

<dl>
<dd>

<dl>
<dd>

**id:** `string` 
    
</dd>
</dl>
</dd>
</dl>


</dd>
</dl>
</details>

<details><summary><code>client.SocialAccounts.ListSlackChannels(ID) -> *schedulin.ListSlackChannelsSocialAccountsResponse</code></summary>
<dl>
<dd>

#### 📝 Description

<dl>
<dd>

<dl>
<dd>

List the channels in a connected Slack workspace that the Schedulin bot can post into (public channels, plus private channels it was invited to). Use an item id as `platformConfiguration.channel` when creating a Slack post.
</dd>
</dl>
</dd>
</dl>

#### 🔌 Usage

<dl>
<dd>

<dl>
<dd>

```go
request := &schedulin.ListSlackChannelsSocialAccountsRequest{
    ID: "id",
}
client.SocialAccounts.ListSlackChannels(
    context.TODO(),
    request,
)
```
</dd>
</dl>
</dd>
</dl>

#### ⚙️ Parameters

<dl>
<dd>

<dl>
<dd>

**id:** `string` 
    
</dd>
</dl>
</dd>
</dl>


</dd>
</dl>
</details>

<details><summary><code>client.SocialAccounts.Update(ID, request) -> *schedulin.UpdateSocialAccountsResponse</code></summary>
<dl>
<dd>

#### 📝 Description

<dl>
<dd>

<dl>
<dd>

Update social media account settings and information
</dd>
</dl>
</dd>
</dl>

#### 🔌 Usage

<dl>
<dd>

<dl>
<dd>

```go
request := &schedulin.UpdateSocialAccountsRequest{
    ID: "id",
}
client.SocialAccounts.Update(
    context.TODO(),
    request,
)
```
</dd>
</dl>
</dd>
</dl>

#### ⚙️ Parameters

<dl>
<dd>

<dl>
<dd>

**id:** `string` 
    
</dd>
</dl>

<dl>
<dd>

**status:** `*schedulin.UpdateSocialAccountsRequestStatus` 
    
</dd>
</dl>
</dd>
</dl>


</dd>
</dl>
</details>

<details><summary><code>client.SocialAccounts.Delete(ID, request) -> *schedulin.DeleteSocialAccountsResponse</code></summary>
<dl>
<dd>

#### 📝 Description

<dl>
<dd>

<dl>
<dd>

Disconnect a social account. By default this is a soft disconnect: the stored credentials are wiped, the account stops counting toward your plan's account limit, and it stays in `GET /v0/social-accounts` with `status: "disconnected"` and `disconnectedReason: "TOKEN_REVOKED"` until it is reconnected from the dashboard. All of its posts, analytics, and history are kept; scheduled posts that come due while it is disconnected fail with a "reconnect" error instead of publishing. Pass `permanent=true` to delete the account instead — this **permanently deletes every post** (scheduled, draft, and published history) of the account and cannot be undone.
</dd>
</dl>
</dd>
</dl>

#### 🔌 Usage

<dl>
<dd>

<dl>
<dd>

```go
request := &schedulin.DeleteSocialAccountsRequest{
    ID: "id",
}
client.SocialAccounts.Delete(
    context.TODO(),
    request,
)
```
</dd>
</dl>
</dd>
</dl>

#### ⚙️ Parameters

<dl>
<dd>

<dl>
<dd>

**id:** `string` 
    
</dd>
</dl>

<dl>
<dd>

**permanent:** `*bool` 
    
</dd>
</dl>
</dd>
</dl>


</dd>
</dl>
</details>

<details><summary><code>client.SocialAccounts.UpdateTimezone(ID, request) -> *schedulin.UpdateTimezoneSocialAccountsResponse</code></summary>
<dl>
<dd>

#### 📝 Description

<dl>
<dd>

<dl>
<dd>

Set the IANA timezone (e.g. 'America/Los_Angeles') used to interpret queue times for this account. Unknown names and UTC-offset strings (e.g. '+05:00') are rejected with 422.
</dd>
</dl>
</dd>
</dl>

#### 🔌 Usage

<dl>
<dd>

<dl>
<dd>

```go
request := &schedulin.UpdateTimezoneSocialAccountsRequest{
    ID: "id",
    Timezone: "timezone",
}
client.SocialAccounts.UpdateTimezone(
    context.TODO(),
    request,
)
```
</dd>
</dl>
</dd>
</dl>

#### ⚙️ Parameters

<dl>
<dd>

<dl>
<dd>

**id:** `string` 
    
</dd>
</dl>

<dl>
<dd>

**timezone:** `string` 
    
</dd>
</dl>
</dd>
</dl>


</dd>
</dl>
</details>

<details><summary><code>client.SocialAccounts.NextSlots(ID) -> *schedulin.NextSlotsSocialAccountsResponse</code></summary>
<dl>
<dd>

#### 📝 Description

<dl>
<dd>

<dl>
<dd>

Return the next available queue slot times (UTC) for a social account, computed from its queue schedule, per-slot capacity, and timezone. Empty when the account has no queue times configured. Use a slot as `scheduledAt`, or pass `action: "queue"` when creating a post to take the next slot automatically.
</dd>
</dl>
</dd>
</dl>

#### 🔌 Usage

<dl>
<dd>

<dl>
<dd>

```go
request := &schedulin.NextSlotsSocialAccountsRequest{
    ID: "id",
}
client.SocialAccounts.NextSlots(
    context.TODO(),
    request,
)
```
</dd>
</dl>
</dd>
</dl>

#### ⚙️ Parameters

<dl>
<dd>

<dl>
<dd>

**id:** `string` 
    
</dd>
</dl>

<dl>
<dd>

**limit:** `*int` 
    
</dd>
</dl>

<dl>
<dd>

**after:** `*string` 
    
</dd>
</dl>
</dd>
</dl>


</dd>
</dl>
</details>

<details><summary><code>client.SocialAccounts.PinterestBoards(ID) -> *schedulin.PinterestBoardsSocialAccountsResponse</code></summary>
<dl>
<dd>

#### 📝 Description

<dl>
<dd>

<dl>
<dd>

List the boards for a connected Pinterest account. Use a board id in `platformConfiguration.board_ids` when creating a Pinterest post.
</dd>
</dl>
</dd>
</dl>

#### 🔌 Usage

<dl>
<dd>

<dl>
<dd>

```go
request := &schedulin.PinterestBoardsSocialAccountsRequest{
    ID: "id",
}
client.SocialAccounts.PinterestBoards(
    context.TODO(),
    request,
)
```
</dd>
</dl>
</dd>
</dl>

#### ⚙️ Parameters

<dl>
<dd>

<dl>
<dd>

**id:** `string` 
    
</dd>
</dl>
</dd>
</dl>


</dd>
</dl>
</details>

<details><summary><code>client.SocialAccounts.TiktokCreatorInfo(ID) -> *schedulin.TiktokCreatorInfoSocialAccountsResponse</code></summary>
<dl>
<dd>

#### 📝 Description

<dl>
<dd>

<dl>
<dd>

Fetch the privacy-level options, duration limits, and interaction settings for a connected TikTok account — required to build a valid `platformConfiguration` when creating a TikTok post.
</dd>
</dl>
</dd>
</dl>

#### 🔌 Usage

<dl>
<dd>

<dl>
<dd>

```go
request := &schedulin.TiktokCreatorInfoSocialAccountsRequest{
    ID: "id",
}
client.SocialAccounts.TiktokCreatorInfo(
    context.TODO(),
    request,
)
```
</dd>
</dl>
</dd>
</dl>

#### ⚙️ Parameters

<dl>
<dd>

<dl>
<dd>

**id:** `string` 
    
</dd>
</dl>
</dd>
</dl>


</dd>
</dl>
</details>

## Tags
<details><summary><code>client.Tags.List() -> *schedulin.ListTagsResponse</code></summary>
<dl>
<dd>

#### 📝 Description

<dl>
<dd>

<dl>
<dd>

Retrieve a list of tags for the authenticated user with optional search filtering
</dd>
</dl>
</dd>
</dl>

#### 🔌 Usage

<dl>
<dd>

<dl>
<dd>

```go
request := &schedulin.ListTagsRequest{}
client.Tags.List(
    context.TODO(),
    request,
)
```
</dd>
</dl>
</dd>
</dl>

#### ⚙️ Parameters

<dl>
<dd>

<dl>
<dd>

**q:** `*string` 
    
</dd>
</dl>

<dl>
<dd>

**limit:** `*int` 
    
</dd>
</dl>
</dd>
</dl>


</dd>
</dl>
</details>

<details><summary><code>client.Tags.Create(request) -> *schedulin.Tag</code></summary>
<dl>
<dd>

#### 📝 Description

<dl>
<dd>

<dl>
<dd>

Create a new tag. Users can have up to 5 tags.
</dd>
</dl>
</dd>
</dl>

#### 🔌 Usage

<dl>
<dd>

<dl>
<dd>

```go
request := &schedulin.CreateTagsRequest{
    Name: "name",
    Color: "color",
}
client.Tags.Create(
    context.TODO(),
    request,
)
```
</dd>
</dl>
</dd>
</dl>

#### ⚙️ Parameters

<dl>
<dd>

<dl>
<dd>

**name:** `string` 
    
</dd>
</dl>

<dl>
<dd>

**color:** `string` 
    
</dd>
</dl>
</dd>
</dl>


</dd>
</dl>
</details>

<details><summary><code>client.Tags.Update(ID, request) -> *schedulin.Tag</code></summary>
<dl>
<dd>

#### 📝 Description

<dl>
<dd>

<dl>
<dd>

Update an existing tag by its ID. Only the tag owner can update their tags.
</dd>
</dl>
</dd>
</dl>

#### 🔌 Usage

<dl>
<dd>

<dl>
<dd>

```go
request := &schedulin.UpdateTagsRequest{
    ID: "id",
}
client.Tags.Update(
    context.TODO(),
    request,
)
```
</dd>
</dl>
</dd>
</dl>

#### ⚙️ Parameters

<dl>
<dd>

<dl>
<dd>

**id:** `string` 
    
</dd>
</dl>

<dl>
<dd>

**name:** `*string` 
    
</dd>
</dl>

<dl>
<dd>

**color:** `*string` 
    
</dd>
</dl>
</dd>
</dl>


</dd>
</dl>
</details>

<details><summary><code>client.Tags.Delete(ID, request) -> *schedulin.Tag</code></summary>
<dl>
<dd>

#### 📝 Description

<dl>
<dd>

<dl>
<dd>

Delete a tag by its ID. Only the tag owner can delete their tags.
</dd>
</dl>
</dd>
</dl>

#### 🔌 Usage

<dl>
<dd>

<dl>
<dd>

```go
request := &schedulin.DeleteTagsRequest{
    ID: "id",
}
client.Tags.Delete(
    context.TODO(),
    request,
)
```
</dd>
</dl>
</dd>
</dl>

#### ⚙️ Parameters

<dl>
<dd>

<dl>
<dd>

**id:** `string` 
    
</dd>
</dl>
</dd>
</dl>


</dd>
</dl>
</details>

## Media
<details><summary><code>client.Media.CreateFromURL(request) -> *schedulin.Media</code></summary>
<dl>
<dd>

#### 📝 Description

<dl>
<dd>

<dl>
<dd>

Downloads a publicly reachable image or video into the media library and returns the media record. Use the returned `url` in `media[].url` when creating a post. Prefer this over the presign flow whenever your client cannot issue a raw HTTP PUT (e.g. an AI agent). The source URL must be public (no auth), http(s), and at most the post upload limit (250 MB); SVG and other active content is rejected.
</dd>
</dl>
</dd>
</dl>

#### 🔌 Usage

<dl>
<dd>

<dl>
<dd>

```go
request := &schedulin.CreateFromURLMediaRequest{
    URL: "url",
}
client.Media.CreateFromURL(
    context.TODO(),
    request,
)
```
</dd>
</dl>
</dd>
</dl>

#### ⚙️ Parameters

<dl>
<dd>

<dl>
<dd>

**url:** `string` 
    
</dd>
</dl>

<dl>
<dd>

**name:** `*string` 
    
</dd>
</dl>

<dl>
<dd>

**alt:** `*string` 
    
</dd>
</dl>

<dl>
<dd>

**contentType:** `*string` 
    
</dd>
</dl>
</dd>
</dl>


</dd>
</dl>
</details>

<details><summary><code>client.Media.Register(request) -> *schedulin.Media</code></summary>
<dl>
<dd>

#### 📝 Description

<dl>
<dd>

<dl>
<dd>

Adds a file you uploaded with POST /v0/media/presign (intent `post`) + HTTP PUT to the media library in place — no second copy is stored — and returns the media record. Pass the presign `key`. The object's type and size are read from storage and must be an allowed image/video/audio type within the post upload limit (250 MB). Idempotent: registering the same key again returns the existing record. Returns 404 when no uploaded object exists for the key in your workspace.
</dd>
</dl>
</dd>
</dl>

#### 🔌 Usage

<dl>
<dd>

<dl>
<dd>

```go
request := &schedulin.MediaRegister{
    Key: "key",
}
client.Media.Register(
    context.TODO(),
    request,
)
```
</dd>
</dl>
</dd>
</dl>

#### ⚙️ Parameters

<dl>
<dd>

<dl>
<dd>

**key:** `string` — The `key` returned by POST /v0/media/presign, after the bytes were PUT to its `url`. The stored media URL for that key is also accepted.
    
</dd>
</dl>

<dl>
<dd>

**name:** `*string` 
    
</dd>
</dl>

<dl>
<dd>

**alt:** `*string` 
    
</dd>
</dl>
</dd>
</dl>


</dd>
</dl>
</details>

<details><summary><code>client.Media.CreateUploadLink(request) -> *schedulin.CreateUploadLinkMediaResponse</code></summary>
<dl>
<dd>

#### 📝 Description

<dl>
<dd>

<dl>
<dd>

Returns a short-lived URL to a page where the user uploads files from their device (or a pasted attachment) straight into the media library. Hand the URL to the user; once they've uploaded, call GET /v0/media (list media, newest first) and reference the returned `url` when creating a post. Use this whenever the file isn't already at a public URL.
</dd>
</dl>
</dd>
</dl>

#### 🔌 Usage

<dl>
<dd>

<dl>
<dd>

```go
request := &schedulin.CreateUploadLinkMediaRequest{}
client.Media.CreateUploadLink(
    context.TODO(),
    request,
)
```
</dd>
</dl>
</dd>
</dl>

#### ⚙️ Parameters

<dl>
<dd>

<dl>
<dd>

**expiresInHours:** `*int` 
    
</dd>
</dl>
</dd>
</dl>


</dd>
</dl>
</details>

<details><summary><code>client.Media.Upload(request) -> *schedulin.Media</code></summary>
<dl>
<dd>

#### 📝 Description

<dl>
<dd>

<dl>
<dd>

Upload raw image, video, or audio bytes directly as multipart/form-data. The file is stored in your media library and the record is returned; use its `url` in `media[].url` when creating a post. When the file part's type is missing or generic (`application/octet-stream`, `text/plain`), the type is detected from the file's bytes, then its filename extension. Max 250 MB; SVG and other active content is rejected. For a file already hosted at a public URL, prefer POST /v0/media/from-url.
</dd>
</dl>
</dd>
</dl>

#### 🔌 Usage

<dl>
<dd>

<dl>
<dd>

```go
request := &schedulin.UploadMediaRequest{
    File: strings.NewReader(
        "",
    ),
}
client.Media.Upload(
    context.TODO(),
    request,
)
```
</dd>
</dl>
</dd>
</dl>


</dd>
</dl>
</details>

<details><summary><code>client.Media.Retrieve(ID) -> *schedulin.Media</code></summary>
<dl>
<dd>

#### 📝 Description

<dl>
<dd>

<dl>
<dd>

Retrieve media information by its ID
</dd>
</dl>
</dd>
</dl>

#### 🔌 Usage

<dl>
<dd>

<dl>
<dd>

```go
request := &schedulin.RetrieveMediaRequest{
    ID: "id",
}
client.Media.Retrieve(
    context.TODO(),
    request,
)
```
</dd>
</dl>
</dd>
</dl>

#### ⚙️ Parameters

<dl>
<dd>

<dl>
<dd>

**id:** `string` 
    
</dd>
</dl>
</dd>
</dl>


</dd>
</dl>
</details>

<details><summary><code>client.Media.Update(ID, request) -> *schedulin.Media</code></summary>
<dl>
<dd>

#### 📝 Description

<dl>
<dd>

<dl>
<dd>

Update media information and metadata
</dd>
</dl>
</dd>
</dl>

#### 🔌 Usage

<dl>
<dd>

<dl>
<dd>

```go
request := &schedulin.UpdateMediaRequest{
    ID: "id",
}
client.Media.Update(
    context.TODO(),
    request,
)
```
</dd>
</dl>
</dd>
</dl>

#### ⚙️ Parameters

<dl>
<dd>

<dl>
<dd>

**id:** `string` 
    
</dd>
</dl>

<dl>
<dd>

**url:** `*string` 
    
</dd>
</dl>

<dl>
<dd>

**mimeType:** `*string` 
    
</dd>
</dl>

<dl>
<dd>

**width:** `*int` 
    
</dd>
</dl>

<dl>
<dd>

**height:** `*int` 
    
</dd>
</dl>

<dl>
<dd>

**size:** `*int` 
    
</dd>
</dl>

<dl>
<dd>

**duration:** `*float64` 
    
</dd>
</dl>
</dd>
</dl>


</dd>
</dl>
</details>

<details><summary><code>client.Media.Delete(ID, request) -> *schedulin.DeleteMediaResponse</code></summary>
<dl>
<dd>

#### 📝 Description

<dl>
<dd>

<dl>
<dd>

Delete a media object and remove its files from storage. Fails with a conflict when the media is attached to any post — remove it from those posts (or delete them) first.
</dd>
</dl>
</dd>
</dl>

#### 🔌 Usage

<dl>
<dd>

<dl>
<dd>

```go
request := &schedulin.DeleteMediaRequest{
    ID: "id",
}
client.Media.Delete(
    context.TODO(),
    request,
)
```
</dd>
</dl>
</dd>
</dl>

#### ⚙️ Parameters

<dl>
<dd>

<dl>
<dd>

**id:** `string` 
    
</dd>
</dl>
</dd>
</dl>


</dd>
</dl>
</details>

<details><summary><code>client.Media.List() -> *schedulin.ListMediaResponse</code></summary>
<dl>
<dd>

#### 📝 Description

<dl>
<dd>

<dl>
<dd>

List media for the organization with page pagination, search, type and tag filters
</dd>
</dl>
</dd>
</dl>

#### 🔌 Usage

<dl>
<dd>

<dl>
<dd>

```go
request := &schedulin.ListMediaRequest{}
client.Media.List(
    context.TODO(),
    request,
)
```
</dd>
</dl>
</dd>
</dl>

#### ⚙️ Parameters

<dl>
<dd>

<dl>
<dd>

**page:** `*int` 
    
</dd>
</dl>

<dl>
<dd>

**limit:** `*int` 
    
</dd>
</dl>

<dl>
<dd>

**q:** `*string` 
    
</dd>
</dl>

<dl>
<dd>

**type_:** `*schedulin.ListMediaRequestType` 
    
</dd>
</dl>

<dl>
<dd>

**tagIDs:** `*string` 
    
</dd>
</dl>

<dl>
<dd>

**tagMode:** `*schedulin.ListMediaRequestTagMode` 
    
</dd>
</dl>
</dd>
</dl>


</dd>
</dl>
</details>

<details><summary><code>client.Media.SetTags(MediaID, request) -> *schedulin.SetTagsMediaResponse</code></summary>
<dl>
<dd>

#### 📝 Description

<dl>
<dd>

<dl>
<dd>

Replace the set of tags attached to a media item with the provided tag IDs
</dd>
</dl>
</dd>
</dl>

#### 🔌 Usage

<dl>
<dd>

<dl>
<dd>

```go
request := &schedulin.SetTagsMediaRequest{
    MediaID: "mediaId",
    TagIDs: []string{
        "tagIds",
    },
}
client.Media.SetTags(
    context.TODO(),
    request,
)
```
</dd>
</dl>
</dd>
</dl>

#### ⚙️ Parameters

<dl>
<dd>

<dl>
<dd>

**mediaID:** `string` 
    
</dd>
</dl>

<dl>
<dd>

**tagIDs:** `[]string` 
    
</dd>
</dl>
</dd>
</dl>


</dd>
</dl>
</details>

<details><summary><code>client.Media.CountByTag() -> *schedulin.CountByTagMediaResponse</code></summary>
<dl>
<dd>

#### 📝 Description

<dl>
<dd>

<dl>
<dd>

Return media counts grouped by tag for the organization
</dd>
</dl>
</dd>
</dl>

#### 🔌 Usage

<dl>
<dd>

<dl>
<dd>

```go
client.Media.CountByTag(
    context.TODO(),
)
```
</dd>
</dl>
</dd>
</dl>


</dd>
</dl>
</details>

<details><summary><code>client.Media.CreatePresignedPost(request) -> *schedulin.PresignedPost</code></summary>
<dl>
<dd>

#### 📝 Description

<dl>
<dd>

<dl>
<dd>

Returns a presigned PUT URL. Upload by issuing an HTTP PUT of the raw file bytes to `url` with a `Content-Type` header matching `contentType`, then reference the returned `key` when creating a post.
</dd>
</dl>
</dd>
</dl>

#### 🔌 Usage

<dl>
<dd>

<dl>
<dd>

```go
request := &schedulin.CreatePresignedPost{
    ContentType: "contentType",
    Key: "key",
}
client.Media.CreatePresignedPost(
    context.TODO(),
    request,
)
```
</dd>
</dl>
</dd>
</dl>

#### ⚙️ Parameters

<dl>
<dd>

<dl>
<dd>

**contentType:** `string` 
    
</dd>
</dl>

<dl>
<dd>

**key:** `string` 
    
</dd>
</dl>

<dl>
<dd>

**size:** `*int` 
    
</dd>
</dl>

<dl>
<dd>

**intent:** `*schedulin.CreatePresignedPostIntent` 
    
</dd>
</dl>
</dd>
</dl>


</dd>
</dl>
</details>

## Platforms
<details><summary><code>client.Platforms.List() -> *schedulin.ListPlatformsResponse</code></summary>
<dl>
<dd>

#### 📝 Description

<dl>
<dd>

<dl>
<dd>

Per-platform posting requirements: caption length limits, media count/type rules, whether `platformConfiguration` is required, its JSON Schema when server-validated, and helper endpoints for fetching dynamic values (e.g. Pinterest boards). Platforms marked `comingSoon` cannot be posted to yet.
</dd>
</dl>
</dd>
</dl>

#### 🔌 Usage

<dl>
<dd>

<dl>
<dd>

```go
client.Platforms.List(
    context.TODO(),
)
```
</dd>
</dl>
</dd>
</dl>


</dd>
</dl>
</details>

## Ai
<details><summary><code>client.Ai.GenerateImage(request) -> *schedulin.GenerateImageAiResponse</code></summary>
<dl>
<dd>

#### 📝 Description

<dl>
<dd>

<dl>
<dd>

Submit an AI image generation job
</dd>
</dl>
</dd>
</dl>

#### 🔌 Usage

<dl>
<dd>

<dl>
<dd>

```go
request := &schedulin.GenerateImageAiRequest{
    Prompt: "prompt",
}
client.Ai.GenerateImage(
    context.TODO(),
    request,
)
```
</dd>
</dl>
</dd>
</dl>

#### ⚙️ Parameters

<dl>
<dd>

<dl>
<dd>

**prompt:** `string` 
    
</dd>
</dl>

<dl>
<dd>

**modelKey:** `*schedulin.GenerateImageAiRequestModelKey` 
    
</dd>
</dl>

<dl>
<dd>

**width:** `*int` 
    
</dd>
</dl>

<dl>
<dd>

**height:** `*int` 
    
</dd>
</dl>
</dd>
</dl>


</dd>
</dl>
</details>

<details><summary><code>client.Ai.GetGeneration() -> *schedulin.AiGeneration</code></summary>
<dl>
<dd>

#### 📝 Description

<dl>
<dd>

<dl>
<dd>

Get the status and details of a generation job
</dd>
</dl>
</dd>
</dl>

#### 🔌 Usage

<dl>
<dd>

<dl>
<dd>

```go
request := &schedulin.GetGenerationAiRequest{
    ID: "id",
}
client.Ai.GetGeneration(
    context.TODO(),
    request,
)
```
</dd>
</dl>
</dd>
</dl>

#### ⚙️ Parameters

<dl>
<dd>

<dl>
<dd>

**id:** `string` 
    
</dd>
</dl>
</dd>
</dl>


</dd>
</dl>
</details>

## Webhooks
<details><summary><code>client.Webhooks.List() -> *schedulin.ListWebhooksResponse</code></summary>
<dl>
<dd>

#### 📝 Description

<dl>
<dd>

<dl>
<dd>

List the organization's webhook endpoints. Signing secrets are masked.
</dd>
</dl>
</dd>
</dl>

#### 🔌 Usage

<dl>
<dd>

<dl>
<dd>

```go
client.Webhooks.List(
    context.TODO(),
)
```
</dd>
</dl>
</dd>
</dl>


</dd>
</dl>
</details>

<details><summary><code>client.Webhooks.Create(request) -> *schedulin.WebhookEndpoint</code></summary>
<dl>
<dd>

#### 📝 Description

<dl>
<dd>

<dl>
<dd>

Register an HTTPS endpoint for event deliveries. The response includes the signing secret ONCE — store it; later reads return a masked value.
</dd>
</dl>
</dd>
</dl>

#### 🔌 Usage

<dl>
<dd>

<dl>
<dd>

```go
request := &schedulin.CreateWebhooksRequest{
    URL: "url",
    Events: []schedulin.CreateWebhooksRequestEventsItem{
        schedulin.CreateWebhooksRequestEventsItemPostPublished,
    },
}
client.Webhooks.Create(
    context.TODO(),
    request,
)
```
</dd>
</dl>
</dd>
</dl>

#### ⚙️ Parameters

<dl>
<dd>

<dl>
<dd>

**url:** `string` 
    
</dd>
</dl>

<dl>
<dd>

**events:** `[]schedulin.CreateWebhooksRequestEventsItem` 
    
</dd>
</dl>

<dl>
<dd>

**description:** `*string` 
    
</dd>
</dl>
</dd>
</dl>


</dd>
</dl>
</details>

<details><summary><code>client.Webhooks.Retrieve(ID) -> *schedulin.WebhookEndpoint</code></summary>
<dl>
<dd>

#### 📝 Description

<dl>
<dd>

<dl>
<dd>

Retrieve one webhook endpoint, including failure counters. The signing secret is masked.
</dd>
</dl>
</dd>
</dl>

#### 🔌 Usage

<dl>
<dd>

<dl>
<dd>

```go
request := &schedulin.RetrieveWebhooksRequest{
    ID: "id",
}
client.Webhooks.Retrieve(
    context.TODO(),
    request,
)
```
</dd>
</dl>
</dd>
</dl>

#### ⚙️ Parameters

<dl>
<dd>

<dl>
<dd>

**id:** `string` 
    
</dd>
</dl>
</dd>
</dl>


</dd>
</dl>
</details>

<details><summary><code>client.Webhooks.Delete(ID, request) -> *schedulin.DeleteWebhooksResponse</code></summary>
<dl>
<dd>

#### 📝 Description

<dl>
<dd>

<dl>
<dd>

Delete a webhook endpoint and its delivery history. Deliveries already in flight are dropped.
</dd>
</dl>
</dd>
</dl>

#### 🔌 Usage

<dl>
<dd>

<dl>
<dd>

```go
request := &schedulin.DeleteWebhooksRequest{
    ID: "id",
}
client.Webhooks.Delete(
    context.TODO(),
    request,
)
```
</dd>
</dl>
</dd>
</dl>

#### ⚙️ Parameters

<dl>
<dd>

<dl>
<dd>

**id:** `string` 
    
</dd>
</dl>
</dd>
</dl>


</dd>
</dl>
</details>

<details><summary><code>client.Webhooks.Update(ID, request) -> *schedulin.WebhookEndpoint</code></summary>
<dl>
<dd>

#### 📝 Description

<dl>
<dd>

<dl>
<dd>

Update URL, subscribed events, description, or enabled state. Re-enabling resets the failure streak.
</dd>
</dl>
</dd>
</dl>

#### 🔌 Usage

<dl>
<dd>

<dl>
<dd>

```go
request := &schedulin.UpdateWebhooksRequest{
    ID: "id",
}
client.Webhooks.Update(
    context.TODO(),
    request,
)
```
</dd>
</dl>
</dd>
</dl>

#### ⚙️ Parameters

<dl>
<dd>

<dl>
<dd>

**id:** `string` 
    
</dd>
</dl>

<dl>
<dd>

**url:** `*string` 
    
</dd>
</dl>

<dl>
<dd>

**events:** `[]schedulin.UpdateWebhooksRequestEventsItem` 
    
</dd>
</dl>

<dl>
<dd>

**description:** `*string` 
    
</dd>
</dl>

<dl>
<dd>

**enabled:** `*bool` 
    
</dd>
</dl>
</dd>
</dl>


</dd>
</dl>
</details>

<details><summary><code>client.Webhooks.RotateSecret(ID, request) -> *schedulin.WebhookEndpoint</code></summary>
<dl>
<dd>

#### 📝 Description

<dl>
<dd>

<dl>
<dd>

Generate a new signing secret for the endpoint and return it ONCE. The old secret stops signing immediately.
</dd>
</dl>
</dd>
</dl>

#### 🔌 Usage

<dl>
<dd>

<dl>
<dd>

```go
request := &schedulin.RotateSecretWebhooksRequest{
    ID: "id",
}
client.Webhooks.RotateSecret(
    context.TODO(),
    request,
)
```
</dd>
</dl>
</dd>
</dl>

#### ⚙️ Parameters

<dl>
<dd>

<dl>
<dd>

**id:** `string` 
    
</dd>
</dl>
</dd>
</dl>


</dd>
</dl>
</details>

<details><summary><code>client.Webhooks.Test(ID, request) -> *schedulin.TestWebhooksResponse</code></summary>
<dl>
<dd>

#### 📝 Description

<dl>
<dd>

<dl>
<dd>

Send a signed `ping` event to the endpoint URL and record it in the delivery history.
</dd>
</dl>
</dd>
</dl>

#### 🔌 Usage

<dl>
<dd>

<dl>
<dd>

```go
request := &schedulin.TestWebhooksRequest{
    ID: "id",
}
client.Webhooks.Test(
    context.TODO(),
    request,
)
```
</dd>
</dl>
</dd>
</dl>

#### ⚙️ Parameters

<dl>
<dd>

<dl>
<dd>

**id:** `string` 
    
</dd>
</dl>
</dd>
</dl>


</dd>
</dl>
</details>

<details><summary><code>client.Webhooks.ListDeliveries(ID) -> *schedulin.ListDeliveriesWebhooksResponse</code></summary>
<dl>
<dd>

#### 📝 Description

<dl>
<dd>

<dl>
<dd>

Delivery history for a webhook endpoint: event, status, attempts, last response code, and payload.
</dd>
</dl>
</dd>
</dl>

#### 🔌 Usage

<dl>
<dd>

<dl>
<dd>

```go
request := &schedulin.ListDeliveriesWebhooksRequest{
    ID: "id",
}
client.Webhooks.ListDeliveries(
    context.TODO(),
    request,
)
```
</dd>
</dl>
</dd>
</dl>

#### ⚙️ Parameters

<dl>
<dd>

<dl>
<dd>

**id:** `string` 
    
</dd>
</dl>

<dl>
<dd>

**limit:** `*int` 
    
</dd>
</dl>

<dl>
<dd>

**page:** `*int` 
    
</dd>
</dl>
</dd>
</dl>


</dd>
</dl>
</details>

