<template>
	<form @submit.prevent="handleSubmit">
		<label for="email">Email: </label>
		<input name="email" type="text" v-model="email" required />
		<br />
		<label for="password">Password: </label>
		<input name="password" type="password" v-model="password" required />
		<span v-show="passwordError">{{ passwordError }}</span>
		<br />
		<label for="role">Role: </label>
		<select name="role" v-model="role">
			<option value="designer">Designer</option>
			<option value="developer">Developer</option>
		</select>
		<br />
		<input type="checkbox" name="terms" v-model="isTermsAccepted" />
		<span>I accept terms and conditions</span>
		<br />
		<div>
			<input type="checkbox" value="dev" v-model="envList" />
			<span>Dev</span>
		</div>
		<div>
			<input type="checkbox" value="test" v-model="envList" />
			<span>Test</span>
		</div>
		<div>
			<input type="checkbox" value="production" v-model="envList" />
			<span>Production</span>
		</div>
		<label for="skills">Skills: </label>
		<input name="skills" type="text" v-model="tempSkill" @keyup="addSkill" />
		<div>
			<button v-for="skill in skills" :key="skill" @click="removeSkill(skill)">
				{{ skill }}
			</button>
		</div>
		<div>
			<button type="submit">Submit</button>
		</div>
	</form>
</template>

<script>
export default {
	data() {
		return {
			email: "",
			password: "",
			role: "designer",
			isTermsAccepted: false,
			envList: [],
			tempSkill: "",
			skills: [],
			passwordError: "",
		};
	},
	methods: {
		addSkill(e) {
			if (e.key === "," && this.tempSkill) {
				if (!this.skills.includes(this.tempSkill)) {
					this.skills.push(this.tempSkill.substring(0, this.tempSkill.length - 1));
					this.tempSkill = "";
				}
			}
		},
		removeSkill(skillToRemove) {
			this.skills = this.skills.filter(skill => skillToRemove !== skill);
		},
		handleSubmit() {
			this.passwordError =
				this.password.length > 5 ? "" : "Please use password more than 5 char length";
			console.log(
				this.email,
				this.password,
				this.role,
				this.isTermsAccepted,
				this.envList,
				this.skills
			);
		},
	},
};
</script>
