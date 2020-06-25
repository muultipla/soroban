---
# Display name
displayName: "{{ replace .Name "-" " " | title }}"

# Username (this should match the folder name and the name on publications)
authors:
- "{{ urlize .Name }}"

slug: "{{ urlize .Name }}"

---
