import base64
import requests


repo_owner = 'your-github-username'  
repo_name = 'your-repository-name' 
file_path = 'bird_image.png' 
commit_message = 'Add image of a bird'  


token = 'your-personal-access-token'


url = f'https://api.github.com/repos/{repo_owner}/{repo_name}/contents/{file_path}'


with open(file_path, 'rb') as image_file:
    image_data = base64.b64encode(image_file.read()).decode('utf-8')


data = {
    'message': commit_message,
    'content': image_data
}


response = requests.put(url, json=data, headers={'Authorization': f'token {token}'})


if response.status_code == 201:
    print(f'Successfully uploaded {file_path} to GitHub.')
else:
    print(f'Failed to upload the file. Error: {response.content}')
