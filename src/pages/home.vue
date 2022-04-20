<template>
	<Form @onSubmit="handleSubmit" />
	<List @onRemove="handleRemove" :items="notes" />
</template>

<script>
import Form from '@/components/Notes/Form.vue'
import List from '@/components/Notes/List.vue'

export default {
	components: { Form, List },
	data() {
		return {
			notes: [
				{
					title: 'Learn Vue 3',
					tags: ['work']
				},
				{
					title: 'Learn Vue 3',
					tags: ['work', 'home']
				},
				{
					title: 'Learn Vue 3',
					tags: []
				}
			]
		}
	},
	watch: {
		notes: {
			handler(updatedList) {
				localStorage.setItem('notes', JSON.stringify(updatedList))
			},
			deep: true
		}
	},
	mounted() {
		this.getNotes()
	},
	methods: {
		getNotes() {
			const localNotes = localStorage.getItem('notes')
			if (localNotes) {
				this.notes = JSON.parse(localNotes)
			}
		},
		handleSubmit({title, selectedTags}) {
			const note = {
				title: title,
				tags: [...selectedTags]
			}
			this.notes.push(note)
		},
		handleRemove(index) {
			this.notes.splice(index, 1)
		}
	}
}
</script>
