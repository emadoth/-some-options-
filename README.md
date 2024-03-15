import os
from git import Repo


github_username = 'your-username'
repository_name = 'GitLab-Exercise'
local_directory = 'path/to/local/directory'
readme_update_text = """# Favorite Git Command
\nMy favorite Git command is `git push` because it allows me to update remote repositories with local commits."""
branch_name = 'feature-branch'


os.system(f'git init {repository_name}')
os.system(f'cd {repository_name} && git remote add origin https://github.com/{github_username}/{repository_name}.git')


repo = Repo.clone_from(
    f'https://github.com/{github_username}/{repository_name}.git',
    local_directory
)
new_branch = repo.create_head(branch_name)
new_branch.checkout()

with open(os.path.join(local_directory, 'README.md'), 'a') as readme_file:
    readme_file.write(readme_update_text)


repo.git.add('README.md')
repo.git.commit('-m', 'Add favorite Git command to README')


origin = repo.remote('origin')
origin.push(branch_name)
