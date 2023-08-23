# Auto Content Generator

The **Auto Content Generator** is an Azure Function developed in C# with the primary objective of utilizing OpenAI's GPT-3.5-turbo model to generate freshly composed blog posts formatted using markdown. While the initial prompt has been preserved here to elucidate the underlying approach, it's imperative to customize it in alignment with the specific prerequisites of your blog. This function is multifaceted in its operation, encompassing the initiation of several key tasks: initiating the cloning of a specified GitHub repository, creating an original Markdown file to accommodate the content of the forthcoming blog post, executing a commit process for the recently generated file, and subsequently triggering the creation of a pull request to seamlessly incorporate this pivotal alteration.

## Environment Variables

To facilitate seamless operation, the Auto Content Generator relies on the following environment variables:

- `GitHubToken`: The personal access token associated with your GitHub account.
- `GitHubRepoOwner`: The proprietor of the targeted GitHub repository.
- `GitHubRepoName`: The designation of the targeted GitHub repository.
- `GitHubEmail`: The email address linked to your GitHub account.
- `GitHubPostsDirectory`: The specific repository directory where blog posts are stored.
- `OpenAIKey`: Your unique API key for OpenAI.

## Usage

To effectively deploy and utilize the Auto Content Generator, follow these steps:

1. Configure the necessary environment variables within the `local.settings.json` file.

Sample `local.settings.json`:

```json
{
  "IsEncrypted": false,
  "Values": {
    "AzureWebJobsStorage": "",
    "FUNCTIONS_WORKER_RUNTIME": "dotnet",
    "GitHubToken": "<your_github_token>",
    "GitHubRepoOwner": "<repository_owner>",
    "GitHubRepoName": "<repository_name>",
    "GitHubEmail": "<github_email>",
    "GitHubPostsDirectory": "<posts_directory>",
    "OpenAIKey": "<your_openai_key>"
  }
}

1. Deploy the function to your Azure environment.
2. Invoke the HTTP trigger whenever a new blog post is desired.
3. Set up the GitHub webhook with the event type "pull_request_review" and configure the payload URL as follows: https://<function_app_name>.azurewebsites.net/api/HandlePullRequestComment?code=<function_code>.