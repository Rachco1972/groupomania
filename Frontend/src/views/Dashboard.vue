<template>
	<div>
		<HeaderNav 
            v-on:switchMode="switchMode"
        />
		<main class="mx-auto px-xs-0 px-sm-3">
            <AllPosts
				v-if="mode === 'dashboard'"
				v-on:switchMode="switchMode"
				v-on:getPostId="getPostId"
			/>
            
			<Post 
                v-if="mode === 'onePost'"
                v-on:switchMode="switchMode"
                :postId="postId"
                :mode="mode"
            />

			<PostForm
				v-if="mode === 'createPost' || mode === 'editPost'"
				v-on:switchMode="switchMode"
                :mode="mode"
                :postId="postId"
			/>

			<Profile 
                v-if="mode === 'profile'" 
                v-on:switchMode="switchMode"
                :mode="mode"
            />

            <Admin
                v-if="mode === 'admin' && $store.state.isAdmin"
            />
		</main>
	</div>
</template>

<script>
import HeaderNav from "@/components/HeaderNav.vue";
import AllPosts from "@/components/AllPosts.vue";
import PostForm from "@/components/PostForm.vue";
import Post from "@/components/Post.vue";
import Profile from "@/components/Profile.vue";
import Admin from "@/components/Admin.vue";

export default {
	name: "Dashboard",
	components: { HeaderNav, AllPosts, PostForm, Post, Profile, Admin },
	data() {
		return {
			modeCreatePost: false,
			mode: "dashboard",
			postId: null,
		};
	},
	methods: {
		switchMode: function(mode) {
			this.mode = mode;
		},
		getPostId: function(postId) {
			this.postId = postId;
		},
	},
};
</script>

<style scoped>
div
 {
    background-color: #e6e6e6;
}
main {
	max-width: 1000px;
    min-height:100vh;
}
</style>
