# The most secure algorithm

Always make sure to generate your ssh keys using *ed25519*
`ssh-keygen -t ed25519`

# Add you ssh keys

Run the agent in the background
`eval "$(ssh-agent -s)" && ssh-add /home/user/.ssh/[PRVT_KEY]`
