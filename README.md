## و برای استفاده در Blazor
### ایجاد یک فایل جدید به نام `ExpandableText.razor` :

```cs
@code {
    private bool isExpanded = false;

    private string ButtonText => isExpanded ? "Less" : "More";

    [Parameter]
    public string FullText { get; set; } = string.Empty;

    [Parameter]
    public int PreviewLength { get; set; } = 300; // Default preview length

    private string DisplayText => isExpanded || FullText.Length <= PreviewLength
        ? FullText
        : FullText.Substring(0, PreviewLength) + "...";

    private string TextClass => isExpanded ? "text-preview expanded" : "text-preview";

    private void ToggleText()
    {
        isExpanded = !isExpanded;
    }
}

<div class="expandable-text">
    <h2>Expandable Text Example</h2>
    <p class="@TextClass">@DisplayText</p>
    <button class="toggle-button" @onclick="ToggleText">@ButtonText</button>
</div>

<style>
    /* General container styling */
    .expandable-text {
        background: linear-gradient(135deg, #ffffff, #f0f0f5);
        border: 1px solid #ddd;
        box-shadow: 0px 4px 10px rgba(0, 0, 0, 0.1);
        padding: 20px 30px;
        border-radius: 12px;
        max-width: 800px;
        width: 100%;
        overflow: hidden;
        position: relative;
        transition: transform 0.5s ease, box-shadow 0.5s ease;
    }

    .expandable-text h2 {
        font-size: 1.8rem;
        margin-bottom: 15px;
        color: #333;
        text-align: center;
        font-weight: bold;
    }

    .text-preview {
        overflow: hidden;
        white-space: nowrap;
        text-overflow: ellipsis;
        max-height: 7.2em;
        color: #555;
        font-size: 1rem;
        position: relative;
        transition: max-height 1s ease, opacity 1s ease;
    }

    .text-preview.expanded {
        max-height: 100vh;
        white-space: normal;
        opacity: 1;
    }

    .text-preview::after {
        content: '';
        position: absolute;
        bottom: 0;
        right: 0;
        width: 100%;
        height: 1.2em;
        background: linear-gradient(to top, #f4f4f9, rgba(244, 244, 249, 0));
        pointer-events: none;
    }

    .text-preview.expanded::after {
        display: none;
    }

    /* Button styling */
    .toggle-button {
        color: #000;
        font-size: 14px;
        font-weight: bold;
        cursor: pointer;
        padding: 10px 20px;
        margin-top: 15px;
        border: none;
        border-radius: 8px;
        display: inline-block;
        transition: background 0.3s ease, transform 0.3s ease;
        box-shadow: 0px 4px 6px rgba(0, 0, 0, 0.1);
    }

    .toggle-button:hover {
        transform: translateY(-2px);
        box-shadow: 0px 6px 10px rgba(0, 0, 0, 0.15);
    }

    .toggle-button:active {
        transform: translateY(1px);
        box-shadow: 0px 2px 4px rgba(0, 0, 0, 0.2);
    }
</style>
```


## استفاده در صفحه ای مثل Index و یا...

```cs

<h1>Welcome to Expandable Text</h1>

<ExpandableText FullText="Lorem ipsum dolor sit amet, consectetur adipiscing elit, sed do eiusmod tempor incididunt ut labore et dolore magna aliqua. Ut enim ad minim veniam, quis nostrud exercitation ullamco laboris nisi ut aliquip ex ea commodo consequat. Duis aute irure dolor in reprehenderit in voluptate velit esse cillum dolore eu fugiat nulla pariatur. Excepteur sint occaecat cupidatat non proident, sunt in culpa qui officia deserunt mollit anim id est laborum." PreviewLength="200" />

```




